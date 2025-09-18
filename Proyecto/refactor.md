```
backend/
├── app/
│   ├── api/
│   │   ├── endpoints/
│   │   │   ├── drivers.py         ← endpoints para pilotos
│   │   │   ├── sessions.py        ← endpoints para sesiones
│   │   │   └── __init__.py
│   │   └── __init__.py
│   ├── core/
│   │   ├── config.py              ← configuración (incluye CORS, etc.)
│   │   └── __init__.py
│   ├── models/
│   │   ├── driver.py              ← modelos de respuesta de pilotos
│   │   ├── session.py             ← modelos de sesión
│   │   └── __init__.py
│   ├── services/
│   │   ├── drivers_service.py     ← lógica para recuperar datos de OpenF1 API
│   │   ├── sessions_service.py
│   │   └── __init__.py
│   ├── main.py                    ← punto de entrada (FastAPI app)
│   └── __init__.py
├── .env                           ← contiene la URL de la API externa (opcional)
├── requirements.txt               ← dependencias (FastAPI, httpx, etc.)
└── README.md
```

### `backend/app/core/config.py`
```python
from fastapi.middleware.cors import CORSMiddleware

def configure_cors(app):
    app.add_middleware(
        CORSMiddleware,
        allow_origins=["*"],
        allow_credentials=True,
        allow_methods=["*"],
        allow_headers=["*"],
    )
```

---

### `backend/app/models/driver.py`
```python
from pydantic import BaseModel

class Driver(BaseModel):
    full_name: str
    number: str
    team: str
    country: str
    headshot_url: str
    team_colour: str
```

---

### `backend/app/models/session.py`
```python
from pydantic import BaseModel

class Session(BaseModel):
    session_key: int
    label: str
    date: str
```

---

### `backend/app/services/drivers_service.py`
```python
import httpx
from unidecode import unidecode
from app.models.driver import Driver

BASE_URL = "https://api.openf1.org/v1"

def generate_f1_headshot_url(full_name: str) -> str:
    name = unidecode(full_name)
    parts = name.strip().split()

    if len(parts) < 2:
        return "https://media.formula1.com/d_driver_fallback_image.png/content/dam/fom-website/drivers"

    first = parts[0]
    last = parts[-1]
    middle = parts[1] if len(parts) > 2 else ""

    code = (first[:3] + last[:3] + "01").upper()
    safe_name = first + "_" + last if not middle else f"{first} {middle}_{last}"
    firstletter = safe_name[0].upper()

    return f"https://www.formula1.com/content/dam/fom-website/drivers/{firstletter}/{code}_{safe_name}/{code.lower()}.png.transform/3col/image.png"

async def fetch_drivers(session_key: int):
    async with httpx.AsyncClient() as client:
        response = await client.get(f"{BASE_URL}/drivers", params={"session_key": session_key})
        response.raise_for_status()
        data = response.json()

    drivers = {}
    for d in data:
        number = d.get("driver_number")
        name = d.get("full_name")
        if not name or not number:
            continue

        key = f"{number}-{name}"
        if key in drivers:
            continue

        headshot = d.get("headshot_url") or ""
        if "/1col/" in headshot:
            headshot = headshot.replace("/1col/", "/3col/")
        if not headshot or not headshot.startswith("http") or not headshot.endswith("3col/image.png"):
            headshot = generate_f1_headshot_url(name)

        drivers[key] = Driver(
            full_name=name,
            team=d.get("team_name") or "Unknown",
            country=d.get("country_code") or "",
            number=str(number),
            headshot_url=headshot,
            team_colour="#" + (d.get("team_colour") or "555555"),
        )

    return list(drivers.values())
```

---

### `backend/app/services/sessions_service.py`
```python
import httpx
from app.models.session import Session

BASE_URL = "https://api.openf1.org/v1"

async def fetch_sessions(year: int):
    async with httpx.AsyncClient() as client:
        response = await client.get(f"{BASE_URL}/sessions", params={"year": year, "session_type": "Race"})
        response.raise_for_status()

    data = response.json()
    return [
        Session(
            session_key=s["session_key"],
            label=f"{s['country_name']} - {s['circuit_short_name']} - {s['session_name']}",
            date=s["date_start"][:10],
        )
        for s in data
    ]
```

---

### `backend/app/api/endpoints/drivers.py`
```python
from fastapi import APIRouter, Query
from app.services.drivers_service import fetch_drivers

router = APIRouter()

@router.get("/drivers")
async def get_drivers(session_key: int = Query(...)):
    return await fetch_drivers(session_key)
```

---

### `backend/app/api/endpoints/sessions.py`
```python
from fastapi import APIRouter, Query
from app.services.sessions_service import fetch_sessions

router = APIRouter()

@router.get("/sessions")
async def get_sessions(year: int = Query(...)):
    return await fetch_sessions(year)
```

---

### `backend/app/main.py`
```python
from fastapi import FastAPI
from app.core.config import configure_cors
from app.api.endpoints.drivers import router as drivers_router
from app.api.endpoints.sessions import router as sessions_router

app = FastAPI()

configure_cors(app)

app.include_router(drivers_router, prefix="/api")
app.include_router(sessions_router, prefix="/api")
```

---

### `backend/.env`
```env
BASE_URL=https://api.openf1.org/v1
```


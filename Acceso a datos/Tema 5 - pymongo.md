```python
from pymongo import MongoClient, ASCENDING
  
client = MongoClient('localhost')  
  
db = client['prueba']  
col = db['personas']  
  
print (client.list_database_names())  
print (db.list_collection_names())  
  
col.insert_one({  
    'edad': 22,  
    'nombre': 'EL CACAS',  
    'intereses': ['PORNO DE GORDAS', 'PAPAS FRITAS']  
    })
    
col.insert_many([{  
        'edad': 10,  
        'nombre': 'EL CULOS',  
        'intereses': ['PORNO DE NEGRAS', 'MUTUMBU']  
    },  
    {  
        'edad': 80,  
        'nombre': 'EL CUCAS',  
        'intereses': ['PORNO DE LATINAS', 'EL NOVIO DE SU ESPOSA']  
    }  
])  
  
print (col.count_documents({}))

doc = col.find_one({  
    "edad": {  
        "$gt": 20  
    }  
})  
print (doc)
doc = col.delete_one({  
    "edad": 20  
})
for document in col.find({}):  
    print(document)
col.update_one({  
    "edad": 80  
}, {  
    "$set": {  
        "edad": 90  
    }  
}) 
col.create_index([('edad', ASCENDING)])

db.drop_collection('personas')

client.drop_database('prueba')

client.close()
```
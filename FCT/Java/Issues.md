Issue 3
```java
package net.aspanc.bootcamp.springmvc.service;  
  
import net.aspanc.bootcamp.springmvc.model.GameModel;  
  
import java.util.List;  
import java.util.Optional;  
  
public interface GameService {  
  
    List<GameModel> findAll();  
  
    Optional<GameModel> findById(Long id);  
  
    List<GameModel> findByTitle(String title);  
  
    void delete(Long id);  
  
    GameModel save(GameModel game);  
}

```

```java
package net.aspanc.bootcamp.springmvc.service;  
  
import net.aspanc.bootcamp.springmvc.model.GameModel;  
import net.aspanc.bootcamp.springmvc.repository.GameRepository;  
import org.springframework.beans.factory.annotation.Autowired;  
import org.springframework.stereotype.Service;  
  
import java.util.List;  
import java.util.Optional;  
  
@Service  
public class GameServiceImpl implements GameService {  
  
    private final GameRepository gameRepository;  
  
    @Autowired  
    public GameServiceImpl(GameRepository gameRepository) {  
        this.gameRepository = gameRepository;  
    }  
  
    @Override  
    public List<GameModel> findAll() {  
        return gameRepository.findAll();  
    }  
  
    @Override  
    public Optional<GameModel> findById(Long id) {  
        return gameRepository.findById(id);  
    }  
  
    @Override  
    public List<GameModel> findByTitle(String title) {  
        return gameRepository.findByTitle(title);  
    }  
  
    @Override  
    public void delete(Long id) {  
        gameRepository.deleteById(id);  
    }  
  
    @Override  
    public GameModel save(GameModel game) {  
        return gameRepository.save(game);  
    }  
}
```

Issue 4
```java
package net.aspanc.bootcamp.springmvc.service.impl;

import net.aspanc.bootcamp.springmvc.model.Game;
import net.aspanc.bootcamp.springmvc.service.GameService;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.annotation.DirtiesContext;
import org.springframework.test.context.ActiveProfiles;
import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;
import org.springframework.transaction.annotation.Transactional;
import java.util.List;
import java.util.Optional;
import static org.junit.Assert.*;

@RunWith(SpringJUnit4ClassRunner.class)
@SpringBootTest
@ActiveProfiles("test") // Use application.properties from test
@Transactional // Ensures rollback after each test
@DirtiesContext(classMode = DirtiesContext.ClassMode.AFTER_EACH_TEST_METHOD)
public class GameServiceImplIntegrationTest {

    @Autowired
    private GameService gameService;

    private Game buildSampleGame() {
        return Game.builder()
                .title("Counter Strike")
                .description("Shooting simulator")
                .steamId(413150)
                .build();
    }

    @Test
    public void testSaveAndFindById() {
        Game game = gameService.save(buildSampleGame());
        Optional<Game> result = gameService.findById(game.getId());

        assertTrue(result.isPresent());
        assertEquals("Counter Strike", result.get().getTitle());
    }

    @Test
    public void testFindByTitle() {
        gameService.save(buildSampleGame());
        List<Game> result = gameService.findByTitle("strike");

        assertEquals(1, result.size());
        assertEquals("Counter Strike", result.get(0).getTitle());
    }

    @Test
    public void testFindAll() {
        gameService.save(buildSampleGame());
        List<Game> result = gameService.findAll();

        assertEquals(1, result.size());
    }

    @Test
    public void testDeleteById() {
        Game game = gameService.save(buildSampleGame());
        gameService.deleteById(game.getId());

        Optional<Game> result = gameService.findById(game.getId());
        assertFalse(result.isPresent());
    }
}
```
Issue 5
```java
package com.example.yourproject.dto;

import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@NoArgsConstructor
@AllArgsConstructor
public class GameDto {

    private Long id;
    private String title;
    private String description;
    private Integer steamId;
}

```
```JAVA
package com.example.yourproject.converter;

import com.example.yourproject.dto.GameDto;
import com.example.yourproject.model.GameModel;
import org.springframework.core.convert.converter.Converter;
import org.springframework.stereotype.Component;

@Component
public class GameModelToGameDtoConverter implements Converter<GameModel, GameDto> {

    @Override
    public GameDto convert(GameModel source) {
        return new GameDto(
            source.getId(),
            source.getTitle(),
            source.getDescription(),
            source.getSteamId()
        );
    }
}


```
Issue 6
```JAVA
package com.example.yourproject.converter;

import com.example.yourproject.dto.GameDto;
import com.example.yourproject.model.GameModel;
import org.springframework.core.convert.converter.Converter;
import org.springframework.stereotype.Component;

@Component
public class GameDtoToGameModelConverter implements Converter<GameDto, GameModel> {

    @Override
    public GameModel convert(GameDto source) {
        return new GameModel(
            source.getId(),
            source.getTitle(),
            source.getDescription(),
            source.getSteamId()
        );
    }
}

```

```JAVA
package com.example.yourproject.converter;

import com.example.yourproject.dto.GameDto;
import com.example.yourproject.model.GameModel;
import org.junit.Before;
import org.junit.Test;

import static org.junit.Assert.*;

public class GameModelToGameDtoConverterTest {

    private GameModelToGameDtoConverter converter;

    @Before
    public void setUp() {
        converter = new GameModelToGameDtoConverter();
    }

    @Test
    public void testConvertGameModelToGameDto() {
        GameModel model = new GameModel(1L, "Test Title", "Test Description", 12345);

        GameDto dto = converter.convert(model);

        assertNotNull(dto);
        assertEquals(model.getId(), dto.getId());
        assertEquals(model.getTitle(), dto.getTitle());
        assertEquals(model.getDescription(), dto.getDescription());
        assertEquals(model.getSteamId(), dto.getSteamId());
    }
}

```
Issue 8
```java
package com.example.yourproject.facade;

import com.example.yourproject.dto.GameDto;
import com.example.yourproject.model.GameModel;
import com.example.yourproject.service.GameService;
import org.springframework.core.convert.converter.Converter;
import org.springframework.stereotype.Component;

import java.util.List;
import java.util.Optional;
import java.util.stream.Collectors;

@Component
public class GameFacade {

    private final GameService gameService;
    private final Converter<GameModel, GameDto> modelToDto;
    private final Converter<GameDto, GameModel> dtoToModel;

    public GameFacade(GameService gameService,
                      Converter<GameModel, GameDto> modelToDto,
                      Converter<GameDto, GameModel> dtoToModel) {
        this.gameService = gameService;
        this.modelToDto = modelToDto;
        this.dtoToModel = dtoToModel;
    }

    public List<GameDto> findAll() {
        return gameService.findAll().stream()
                .map(modelToDto::convert)
                .collect(Collectors.toList());
    }

    public GameDto findById(Long id) {
        Optional<GameModel> gameModel = gameService.findById(id);
        return gameModel.map(modelToDto::convert).orElse(null);
    }

    public List<GameDto> findByTitle(String title) {
        return gameService.findByTitle(title).stream()
                .map(modelToDto::convert)
                .collect(Collectors.toList());
    }

    public void delete(Long id) {
        gameService.delete(id);
    }

    public GameDto save(GameDto gameDto) {
        GameModel model = dtoToModel.convert(gameDto);
        GameModel saved = gameService.save(model);
        return modelToDto.convert(saved);
    }
}

```
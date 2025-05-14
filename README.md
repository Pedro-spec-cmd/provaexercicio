# provaexercicio# # Exemplo de Navegação Completa com Formulário usando `asyncStoryge`

Este projeto demonstra como implementar uma navegação completa entre telas, incluindo um formulário, utilizando a função `asyncStoryge` para navegação assíncrona e gerenciamento de dados.

## Funcionalidades

- ![🏠](https://em-content.zobj.net/thumbs/120/apple/354/house_1f3e0.png) Navegação entre telas (Home, Formulário e Resultado)
- ![📝](https://em-content.zobj.net/thumbs/120/apple/354/memo_1f4dd.png) Formulário com validação de campos
- ![💾](https://em-content.zobj.net/thumbs/120/apple/354/floppy-disk_1f4be.png) Uso de `asyncStoryge` para salvar e recuperar dados de forma assíncrona
- ![👀](https://em-content.zobj.net/thumbs/120/apple/354/eyes_1f440.png) Exibição dos dados enviados após o envio do formulário

## Estrutura das Telas

### 1. Tela Inicial (Home)

Permite ao usuário navegar para o formulário.

```javascript
// HomeScreen.js
import React from 'react';
import { Button, View } from 'react-native';

export default function HomeScreen({ navigation }) {
  return (
    <View>
      <Button
        title="Preencher Formulário"
        onPress={() => navigation.navigate('FormScreen')}
      />
    </View>
  );
}
```

### 2. Tela do Formulário

Coleta dados do usuário e salva usando `asyncStoryge`.

```javascript
// FormScreen.js
import React, { useState } from 'react';
import { Button, TextInput, View, Alert } from 'react-native';
import { saveData } from './utils/asyncStoryge';

export default function FormScreen({ navigation }) {
  const [nome, setNome] = useState('');

  const handleSubmit = async () => {
    if (!nome) {
      Alert.alert('Preencha o nome!');
      return;
    }
    await saveData('userName', nome);
    navigation.navigate('ResultScreen');
  };

  return (
    <View>
      <TextInput
        placeholder="Digite seu nome"
        value={nome}
        onChangeText={setNome}
      />
      <Button title="Enviar" onPress={handleSubmit} />
    </View>
  );
}
```

### 3. Tela de Resultado

Recupera e exibe os dados salvos.

```javascript
// ResultScreen.js
import React, { useEffect, useState } from 'react';
import { Text, View } from 'react-native';
import { getData } from './utils/asyncStoryge';

export default function ResultScreen() {
  const [nome, setNome] = useState('');

  useEffect(() => {
    async function fetchData() {
      const savedName = await getData('userName');
      setNome(savedName);
    }
    fetchData();
  }, []);

  return (
    <View>
      <Text>Nome enviado: {nome}</Text>
    </View>
  );
}
```

### 4. Utilitário `asyncStoryge`

```javascript
// utils/asyncStoryge.js
import AsyncStorage from '@react-native-async-storage/async-storage';

export async function saveData(key, value) {
  await AsyncStorage.setItem(key, value);
}

export async function getData(key) {
  return await AsyncStorage.getItem(key);
}
```

## Como executar

1. Instale as dependências:  
   ![⬇️](https://em-content.zobj.net/thumbs/120/apple/354/down-arrow_2b07-fe0f.png)
   ```
   npm install
   ```
2. Execute o projeto:  
   ![▶️](https://em-content.zobj.net/thumbs/120/apple/354/play-button_25b6-fe0f.png)
   ```
   npm start
   ```

---

Adapte este exemplo conforme a necessidade do seu projeto!

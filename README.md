
# 🛗 Elevador em Miniatura com Arduino

Este repositório contém o projeto de um **elevador em miniatura** controlado por **Arduino UNO**, que utiliza **Reed Switches (sensores magnéticos)** e **botões físicos** para simular a lógica de funcionamento de um elevador real de quatro níveis (Térreo + 3 andares).

---

## 📦 Funcionalidades

- 🧲 Controle de posição com **3 sensores magnéticos** (Reed Switch)
- 🔘 Seleção de andares com **4 botões físicos**
- ⚙️ Motor DC controlado por **L293/L298**
- 🧠 Lógica programada em Arduino C++
- 🚦 Estrutura de decisão para parada precisa em cada andar

---

## 🧰 Componentes Utilizados

| Quantidade | Componente               |
|------------|---------------------------|
| 1x         | Arduino UNO               |
| 1x         | Motor DC                  |
| 1x         | Driver L293 ou L298       |
| 3x         | Reed Switch (Sensor magnético) |
| 4x         | Botões (Térreo, 1º, 2º e 3º) |
| Cabos, resistores, estrutura do elevador, fonte externa |

---

## 🔧 Esquema de Conexão

- **Botões** conectados a pinos digitais com `INPUT_PULLUP`
- **Reed switches** conectados entre GND e entradas digitais
- **Motor DC** ligado ao driver L293/L298
- **Fonte externa** recomendada para o motor

---

## 🧠 Como Funciona

### 🏁 Início

O sistema espera o usuário pressionar um dos botões:

```cpp
terreo = digitalRead(bterreo);
if (terreo == valorBotoes) {
  botaoandar = 0;
}
```

### 🧲 Detectando o Andar Atual

```cpp
byte andar(){
  if (digitalRead(reedswitch1) == LOW) return 0;
  else if (digitalRead(reedswitch2) == LOW) return 1;
  else if (digitalRead(reedswitch3) == LOW) return 2;
  else if (digitalRead(reedswitch4) == LOW) return 3;
  else return 4;
}
```

### 🔼 Subida / 🔽 Descida / ⏹ Parada

```cpp
void sobe() {
  analogWrite(motorB1, 0);
  analogWrite(motorB2, vSpeed);
}

void desce() {
  analogWrite(motorB1, vSpeed);
  analogWrite(motorB2, 0);
}

void parado() {
  analogWrite(motorB1, 0);
  analogWrite(motorB2, 0);
}
```

### 🚦 Lógica de Decisão

O elevador sobe ou desce automaticamente até atingir o andar desejado:

```cpp
if (botaoandar > andar()) {
  while (botaoandar != andar()) {
    sobe();
  }
}
if (botaoandar < andar()) {
  while (botaoandar != andar()) {
    desce();
  }
}
```

---



## 📸 Imagens 


```markdown
[Protótipo do Elevador](https://github.com/Kaycoala/Projeto-Elevador/issues/1#issue-3194097474)
```

---

## 👨‍💻 Autor

**Kayque da Silva Cremonini**

---

## 🪪 Licença

Este projeto é de uso educacional. Você pode utilizar, modificar e compartilhar livremente com os devidos créditos.

---

## 🌟 Contribua!

Pull requests e sugestões são bem-vindos! Se você tiver melhorias, correções ou quiser ajudar a documentar com imagens, fique à vontade.

---

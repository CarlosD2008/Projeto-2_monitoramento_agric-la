# 🌱 Estufa IoT

Projeto de IoT para monitoramento de uma mini-estufa agrícola usando **ESP32 + DHT22 + LDR + LEDs + Buzzer + Wi-Fi + ThingSpeak**.

## 🎯 Objetivo

Monitorar:

- 🌡️ Temperatura
- 💧 Umidade
- ☀️ Luminosidade
- 🚨 Situação de alerta

O sistema sinaliza a condição por LEDs e buzzer e pode enviar os dados para o ThingSpeak.

## 🔌 Ligações

| Componente | ESP32 |
|---|---:|
| DHT22 DATA | GPIO 15 |
| LDR AO | GPIO 34 |
| LDR DO | GPIO 13 |
| LED verde | GPIO 2 |
| LED vermelho | GPIO 4 |
| Buzzer | GPIO 5 |
| DHT22 VCC | 3V3 |
| LDR VCC | 3V3 |
| GNDs | GND |

## 🧠 Regras

- Temperatura normal: 18°C a 30°C
- Umidade normal: 40% a 80%
- LDR DO HIGH = escuro = alerta
- Qualquer condição fora dos limites gera alerta.
- Normal: LED verde ligado e buzzer desligado.
- Alerta: LED vermelho ligado e buzzer ligado.

## 🧪 Condição inicial do Wokwi

- Temperatura: 25°C
- Umidade: 60%
- LDR: 400 lux

Esperado:

```text
NORMAL
LED VERDE = ligado
LED VERMELHO = desligado
BUZZER = desligado
```

## 🧪 Testes

### Teste de temperatura

No DHT22, altere para:

```text
35°C
```

Esperado:

```text
ALERTA
Motivos: temperatura
LED vermelho ligado
Buzzer ligado
```

### Teste de umidade

Altere para:

```text
20%
```

Esperado:

```text
ALERTA
Motivos: umidade
```

### Teste de luminosidade

Altere o nível de luz do LDR para uma condição escura.

Esperado:

```text
ALERTA
Motivos: luminosidade
```

## ☁️ ThingSpeak

O código já está preparado para enviar:

- Field 1 = temperatura
- Field 2 = umidade
- Field 3 = luminosidade (%)
- Field 4 = status (0 normal / 1 alerta)

Para habilitar:

```cpp
const char* THINGSPEAK_API_KEY = "SUA_WRITE_API_KEY";
```

A URL correta usada pelo ESP32 é:

```text
http://api.thingspeak.com/update
```

Sem uma API Key, o projeto continua funcionando localmente.

## ▶️ Como importar no Wokwi

1. Crie um projeto **ESP32** no Wokwi.
2. Substitua o conteúdo de `sketch.ino`.
3. Substitua o conteúdo de `diagram.json`.
4. Crie/atualize `libraries.txt` com:
   `DHTesp`
5. Inicie a simulação.
6. Abra o Serial Monitor em **115200 baud**.

## ✅ Checklist de validação

- [x] DHT22 no GPIO 15
- [x] LDR AO no GPIO 34
- [x] LDR DO no GPIO 13
- [x] LED verde no GPIO 2
- [x] LED vermelho no GPIO 4
- [x] Buzzer no GPIO 5
- [x] Resistores de 220 ohms nos LEDs
- [x] Wi-Fi Wokwi-GUEST
- [x] URL ThingSpeak corrigida
- [x] JSON sem escapes inválidos
- [x] LED verde sem atributo `flip`
- [x] DHTesp declarado em `libraries.txt`
- [x] Envio cloud a cada 15 segundos

> Observação: a simulação local funciona sem ThingSpeak. O envio para a nuvem depende de uma Write API Key válida.



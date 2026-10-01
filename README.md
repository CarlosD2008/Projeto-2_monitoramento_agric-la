# 🌱 Estufa IoT

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:16a085,100:2ecc71&height=160&section=header&text=🌱%20Estufa%20IoT&fontSize=40&fontColor=fff&animation=fadeIn" width="100%"/>

### 🤖 Monitoramento inteligente de uma miniestufa com ESP32

<img src="https://img.shields.io/badge/ESP32-IoT-2ecc71?style=for-the-badge&logo=espressif&logoColor=white"/>
<img src="https://img.shields.io/badge/DHT22-Temperatura%20%7C%20Umidade-orange?style=for-the-badge"/>
<img src="https://img.shields.io/badge/LDR-Luminosidade-yellow?style=for-the-badge"/>
<img src="https://img.shields.io/badge/ThingSpeak-Cloud-purple?style=for-the-badge"/>

<br><br>

<a href="https://wokwi.com/projects/476135821618994177">
<img src="https://img.shields.io/badge/▶️%20SIMULAR%20NO%20WOKWI-27ae60?style=for-the-badge"/>
</a>

</div>

---

## 🌱 Sobre

Projeto de **IoT agrícola** desenvolvido com **ESP32** para monitorar uma miniestufa em tempo real.

O sistema verifica:

* 🌡️ Temperatura
* 💧 Umidade
* ☀️ Luminosidade
* 🚨 Condições de alerta

Quando algum valor está fora do limite, o sistema ativa **LED vermelho + buzzer**.

---

## ⚙️ Como funciona?

```text
🌡️ DHT22 ──┐
💧 DHT22 ──┤
☀️ LDR ────┤
           ↓
       🧠 ESP32
           ↓
    ┌──────┴──────┐
    ↓             ↓
 🟢 NORMAL     🔴 ALERTA
    ↓             ↓
 LED Verde    LED Vermelho
                +
             🔊 Buzzer
           │
           ↓
       ☁️ ThingSpeak
```

---

## 🧠 Regras do Sistema

| Monitoramento   | Normal            | Alerta               |
| --------------- | ----------------- | -------------------- |
| 🌡️ Temperatura | `18°C – 30°C`     | Fora do limite       |
| 💧 Umidade      | `40% – 80%`       | Fora do limite       |
| ☀️ LDR          | Iluminação normal | `DO = HIGH` / escuro |

### 🟢 Normal

`LED Verde ON` • `LED Vermelho OFF` • `Buzzer OFF`

### 🔴 Alerta

`LED Verde OFF` • `LED Vermelho ON` • `Buzzer ON`

---

## 🔌 Ligações

| Componente      | GPIO |
| --------------- | ---- |
| 🌡️ DHT22       | `15` |
| ☀️ LDR AO       | `34` |
| ☀️ LDR DO       | `13` |
| 🟢 LED Verde    | `2`  |
| 🔴 LED Vermelho | `4`  |
| 🔊 Buzzer       | `5`  |

**VCC → 3V3** • **GND → GND** • **LEDs → resistor 220Ω**

---

## 🧪 Teste Rápido

### 🟢 Estado inicial

```text
🌡️ 25°C
💧 60%
☀️ 400 lux

       ↓

🟢 NORMAL
```

### 🔴 Teste de alerta

Altere qualquer condição:

```text
🌡️ 35°C  → 🚨 ALERTA
💧 20%   → 🚨 ALERTA
🌑 Escuro → 🚨 ALERTA
```

---

## ☁️ ThingSpeak

Os dados podem ser enviados para a nuvem:

```text
Field 1 → 🌡️ Temperatura
Field 2 → 💧 Umidade
Field 3 → ☀️ Luminosidade
Field 4 → 🚨 Status
```

```cpp
const char* THINGSPEAK_API_KEY = "SUA_WRITE_API_KEY";
```

Sem API Key, o projeto continua funcionando normalmente no **Wokwi**.

---

## ▶️ Executar

1. Abra o projeto no **Wokwi**.
2. Configure `sketch.ino`.
3. Configure `diagram.json`.
4. Em `libraries.txt`, adicione:

```text
DHTesp
```

5. Inicie a simulação.
6. Abra o **Serial Monitor — 115200 baud**.

---

## 🛠️ Tecnologias

<div align="center">

`ESP32` • `C++` • `DHT22` • `LDR` • `Wi-Fi` • `ThingSpeak` • `Wokwi`

</div>

---

<div align="center">

### 🌱 Sensores → 🧠 ESP32 → 🚨 Decisão → ☁️ Cloud

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:16a085,100:2ecc71&height=100&section=footer&animation=fadeIn" width="100%"/>

**Desenvolvido por Carlos Daniel**

### link o projeto: 
https://wokwi.com/projects/476135821618994177

</div>

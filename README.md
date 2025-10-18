# 🍷 Vinheria Agnello - Sistema IoT de Monitoramento Ambiental

## 🧠 Descrição do Projeto

Este projeto faz parte do **Checkpoint 2 de Engenharia de Software (Edge Computing & Computer Systems)** e tem como objetivo automatizar o monitoramento de uma **vinheria inteligente**, controlando **luminosidade, temperatura e umidade** em tempo real, utilizando **sensores conectados ao ESP32** e integração via **MQTT**.  

A solução permite visualizar as condições do ambiente e **acionar alertas automáticos** (LEDs e buzzer) conforme as medições, além de permitir **controle manual via MQTT**.

🔗 **Simulação completa no Wokwi:**  
👉 [Clique aqui para visualizar o projeto](https://wokwi.com/projects/444390454504166401)

---

## ⚙️ Funcionalidades

- 📡 Conexão automática com **Wi-Fi** e **broker MQTT**  
- 🌡️ Leitura de **temperatura e umidade (DHT22)**  
- 💡 Monitoramento de **luminosidade (LDR)**  
- 🔔 **Alertas visuais e sonoros** com LEDs e buzzer  
- 🖥️ Exibição dinâmica no **LCD I2C (16x2)**  
- 🔄 Alternância entre **modo automático** e **manual (via MQTT)**  
- 💬 Publicação contínua de dados para tópicos MQTT (compatível com **FIWARE**)  

---

## 🧩 Componentes Utilizados

| Componente         | Função Principal                      | Pino ESP32 |
|--------------------|---------------------------------------|-------------|
| **DHT22**          | Sensor de temperatura e umidade        | 4           |
| **LDR**            | Sensor de luminosidade                 | 34 (ADC)    |
| **LED Verde**      | Indica condição normal                 | 15          |
| **LED Amarelo**    | Indica atenção                         | 5           |
| **LED Vermelho**   | Indica alerta                          | 17          |
| **Buzzer**         | Alarme sonoro                          | 19          |
| **LCD I2C (0x27)** | Exibe mensagens e leituras             | I2C padrão  |
| **ESP32**          | Microcontrolador principal             | —           |

---

## 🌐 Conexão MQTT

- **Broker:** `107.22.140.214`  
- **Porta:** `1883`  
- **Device ID:** `fiware_001`  

### 📤 Publicação (Publish)

| Tópico | Dado Enviado |
|--------|---------------|
| `/TEF/device007/attrs` | Estado do buzzer (`on/off`) |
| `/TEF/device007/attrs/l` | Luminosidade (lux) |
| `/TEF/device007/attrs/t` | Temperatura (°C) |
| `/TEF/device007/attrs/u` | Umidade (%) |

### 📥 Subscrição (Subscribe)

| Tópico | Comando |
|--------|----------|
| `/TEF/device007/cmd` | Recebe mensagens de controle |

### 🔧 Comandos MQTT Aceitos

| Comando | Ação |
|----------|------|
| `device007@on|` | Liga manualmente o buzzer |
| `device007@off|` | Desliga manualmente o buzzer |
| `device007@auto|` | Retorna ao modo automático |

---

## 🧠 Lógica de Funcionamento

### 🔆 Luminosidade
- **≤ 60 lux:** Ambiente ideal → LED verde  
- **60–100 lux:** Meia-luz → LED amarelo  
- **≥ 100 lux:** Muito claro → LED vermelho + buzzer  

### 🌡️ Temperatura
- **10°C a 15°C:** Ideal  
- **> 15°C:** Temperatura alta → alerta  
- **< 10°C:** Temperatura baixa → alerta  

### 💧 Umidade
- **50% a 70%:** Ideal  
- **< 50%:** Umidade baixa → alerta  
- **> 70%:** Umidade alta → alerta  

Durante alertas, o sistema emite som pelo **buzzer** e destaca mensagens prioritárias no **LCD**.

---

## 🧰 Estrutura do Código

O código está dividido em seções principais:

1. ⚙️ **Configurações iniciais:** Wi-Fi, MQTT e sensores  
2. 📈 **Funções de leitura:** sensores DHT22 e LDR  
3. 🖥️ **Exibição:** controle de mensagens e prioridades no LCD  
4. 🔔 **Decisões:** controle de LEDs e buzzer  
5. 🔄 **Loop principal:** atualização contínua e envio MQTT  

---

## 🚀 Como Executar

### ✅ Passo 1 — Acesse o projeto online
Abra o simulador no Wokwi:  
🔗 [https://wokwi.com/projects/444390454504166401](https://wokwi.com/projects/444390454504166401)

### ✅ Passo 2 — Configure o Wi-Fi
O código já utiliza o Wi-Fi padrão do Wokwi:

const char* default_SSID = "Wokwi-GUEST";
const char* default_PASSWORD = ""

✅ Passo 3 — Inicie a simulação

Clique em “Start Simulation” e observe:

📟 Dados no LCD

💡 Mudança de LEDs conforme sensores

🌐 Publicações MQTT no broker

------Conexao WI-FI------
Conectando-se na rede: Wokwi-GUEST
Conectado com sucesso!
Temp: 13.5°C | Umid: 65.2% | Lux: 78
Estado enviado ao broker: ON
Modo atual: AUTOMÁTICO

👥 Autores

Equipe:

Matheus von Koss Wildeisen

Ana Clara Rocha de Oliveira

Deivid Ruan Marques

Felipe Cordeiro

📚 Projeto acadêmico — Engenharia de Software (Edge Computing)

# Circuito RC com Arduino

Este projeto tem como objetivo analisar o comportamento da **carga e descarga de um capacitor** em um circuito RC utilizando o **Arduino UNO** para leitura dos valores de tensão e posterior geração de gráficos representativos.

---

## Descrição do Projeto

O circuito RC é composto por um resistor e um capacitor conectados em série.  
O Arduino é utilizado para **ler a tensão** no ponto entre o resistor e o capacitor (porta analógica A0), enviando os dados pela porta serial.  
Com base nesses dados, foram gerados gráficos que mostram a variação da tensão no resistor e no capacitor ao longo do tempo.

---

## Circuito Montado

A montagem foi feita em uma protoboard conforme o vídeo abaixo:

### Vídeo do Circuito

https://github.com/user-attachments/assets/9268ad1e-e121-4e24-ada3-e38ca53b38ed

**Componentes utilizados:**
- 1x Arduino Uno  
- 1x Resistor (10kΩ)  
- 1x Capacitor eletrolítico (100 µF)
- 1x Interruptor deslizante
- 1x Protoboard

---

## 💻 Código Utilizado

```cpp
int pinoNoRC = 0; 
int valorLido = 0;
float tensaoCapacitor = 0, tensaoResistor;
unsigned long time; 

void setup(){ 
  Serial.begin(9600); 
} 

void loop() { 
  time = millis(); 
  valorLido = analogRead(pinoNoRC); 
  tensaoResistor = (valorLido * 5.0 / 1023); // 5.0V / 1023 degraus = 0.0048876 
  tensaoCapacitor = abs(5.0 - tensaoResistor);
  
  Serial.print(time); 
  Serial.print(" Resistor: "); 
  Serial.print(tensaoResistor);
  Serial.print(" Capacitor: ");
  Serial.println(tensaoCapacitor); 

  delay(400); 
}
```

## Analise dos resultados obtidos

Os gráficos apresentados demonstram o comportamento típico de um circuito RC (resistor-capacitor) durante o processo de carga e descarga do capacitor.

### Comparação entre as tensões no resistor e no capacitor

<img width="800" height="500" alt="comparison" src="https://github.com/user-attachments/assets/41273aef-fc6c-446c-bb42-719255892096" />

Neste gráfico, observamos:
- A linha azul representa a tensão no resistor (VR), que inicia em aproximadamente 5V e decresce exponencialmente com o tempo.  
- A linha laranja representa a tensão no capacitor (VC), que parte de 0V e aumenta gradualmente até se aproximar de 5V.  

Esse comportamento ocorre porque, no início, o capacitor está descarregado e a corrente no circuito é máxima. À medida que o capacitor acumula carga, a corrente diminui e, consequentemente, a queda de tensão no resistor se reduz.

---

### Gráficos separados: carga e descarga

<img width="1200" height="400" alt="separated" src="https://github.com/user-attachments/assets/575c30f7-a12d-450c-b162-22f01ed61928" />

No gráfico à esquerda, observamos a tensão no capacitor (VC) durante a carga:
- A curva apresenta um crescimento exponencial que tende a se estabilizar quando o capacitor se aproxima da carga total.
- Esse comportamento é regido pela constante de tempo do circuito, dada por τ = R × C.

No gráfico à direita, vemos a tensão no resistor (VR) durante a descarga:
- O valor inicial é alto e decresce exponencialmente à medida que o capacitor se carrega.
- Essa variação reflete a diminuição da corrente no circuito com o passar do tempo.

Essas relações evidenciam a natureza exponencial da carga e descarga no circuito RC, confirmando o comportamento observado experimentalmente.

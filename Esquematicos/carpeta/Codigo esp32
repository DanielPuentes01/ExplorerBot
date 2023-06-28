import socket
from wifiAP import apConfig as connect
from machine import Pin
import time
serverAddressPort = socket.getaddrinfo("0.0.0.0", 3000)[0][-1]
bufferSize = 128
connect("miRed", "87654321")

motor_1_Adelante= Pin(32,Pin.OUT)
motor_1_Atras= Pin(27,Pin.OUT)
motor_2_Adelante= Pin(33,Pin.OUT)
motor_2_Atras= Pin(25,Pin.OUT)
trigger_pin=Pin(26,Pin.OUT)
echo_pin=Pin(35,Pin.IN)
sensor_1 = Pin(34, Pin.IN)
señal_camara= Pin(14,Pin.OUT)
leds_rojo=Pin(12,Pin.OUT)
leds_rojo.value(1)
def exec(data):
        señal_camara.value(1)
        if data == b'A' :
            print("Arriba")
            motor_1_Adelante.value(1)
            motor_2_Adelante.value(1)
            leds_rojo.value(0)
            print (motor_2_Adelante.value())
        elif data == b'B':
            motor_1_Atras.value(1)
            motor_2_Atras.value(1)
            leds_rojo.value(1)
            print("Abajo")
        elif data == b'C' :
            motor_1_Adelante.value(1)
            leds_rojo.value(0)
            print("Izquierda")
        elif data == b'D':
            motor_2_Adelante.value(1)
            leds_rojo.value(0)
            print("Derecha")
        elif data == b'E':
            motor_1_Adelante.value(0)
            motor_2_Adelante.value(0)
            motor_1_Atras.value(0)
            motor_2_Atras.value(0)
            print("Detener")
        else:
            print("Obstaculo")

sk = socket.socket()
sk.bind(serverAddressPort)
sk.listen(1)
print("Listening on: ", serverAddressPort)

while True:
    conn, addr = sk.accept()
    while True:
        data = conn.recv(bufferSize)

        if data :
            exec(data)
            conn.sendall("ok")
        else:
            señal_camara.value(0)
            motor_1_Adelante.value(0)
            motor_2_Adelante.value(0)
            motor_1_Atras.value(0)
            motor_2_Atras.value(0)
    conn.close() 

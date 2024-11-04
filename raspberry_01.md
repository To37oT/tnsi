```python
import RPi.GPIO as GPIO
import tkinter as tk
from random import choice
import time
import threading

# Initialisation du GPIO
GPIO.setmode(GPIO.BCM)
GPIO.setup(4, GPIO.IN, pull_up_down=GPIO.PUD_UP)
GPIO.setup(17, GPIO.IN, pull_up_down=GPIO.PUD_UP)
GPIO.setup(27, GPIO.IN, pull_up_down=GPIO.PUD_UP)

running = True

square_x = 150
square_y = 150

# Fonction pour changer la couleur de fond
def change_color():
    colors = ["red", "blue", "green", "yellow", "purple", "orange"]
    new_color = choice(colors)
    canvas.configure(bg=new_color)

def move_left():
    global square_x
    if square_x > 0:
        canvas.move(square, -5, 0)

def move_right():
    global square_x
    if square_x < 290:
        canvas.move(square, 5, 0)
        
# Fonction appelée quand le bouton est pressé
def check_button():
    global running
    while running:
     if GPIO.input(4) == GPIO.LOW:
         change_color()
         time.sleep(0.5)
         
     if GPIO.input(17) == GPIO.LOW:
         move_left()
         time.sleep(0.1)
         
     if GPIO.input(27) == GPIO.LOW:
         move_right()
         time.sleep(0.1)
         
def close_window():
    global running
    running = False
    time.sleep(1) #pour que le thread se terminefaire un ca
    GPIO.cleanup()
    window.destroy()

# Configurer une interruption pour détecter les pressions de bouton
#GPIO.add_event_detect(4, GPIO.RISING, callback=button_pressed, bouncetime=300)

         
# Interface graphique avec Tkinter
window = tk.Tk()
window.title("TP Raspberry Pi")
window.geometry("400x400")

canvas = tk.Canvas(window, width=400, height=400, bg="white")
canvas.pack()

square = canvas.create_rectangle(square_x, square_y, square_x + 10, square_y + 10, fill="black")

button_thread = threading.Thread(target=check_button)
button_thread.daemon = True
button_thread.start()

window.protocol("WM_DELETE_WINDOW", close_window)

# Boucle principale de l'interface
window.mainloop()


# Nettoyage des GPIO à la fin du programme
GPIO.cleanup()
```

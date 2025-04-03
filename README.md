# AnalogClock_Pyhton

import tkinter as tk
from datetime import datetime
import math

class AnalogClockApp:

    def __init__(self,root):
      
        self.root = root
        self.root.title("Analog Clock")
      
        self.canvas = tk.Canvas(self.root, width=300,height=300,bg="white")
        self.canvas.pack()

     
        self.root.after(100, self.draw_clock)
    


    def draw_clock(self):

               
                self.canvas.delete("all")

              
                width = self.canvas.winfo_width()
                height = self.canvas.winfo_height()

               
                center_x = width // 2
                center_y = height // 2

                
                clock_radius = min(width, height) // 2 - 10
                self.canvas.create_oval(center_x - clock_radius, 
                                        center_y - clock_radius,
                                        center_x + clock_radius, 
                                        center_y + clock_radius,
                                        outline = "orange", width = 5)
                

              
                for i in range(1, 13):
                   
                    angle = math.radians(360 / 12 * (i - 3))
                   
                    num_x = center_x + int(clock_radius * 0.8 * math.cos(angle))
                    
                    num_y = center_y + int(clock_radius * 0.8 * math.sin(angle))
                   
                    self.canvas.create_text(num_x, num_y, text=str(i), 
                    font=("Helvetica", 12, "bold"))

               
                current_time = datetime.now()
                
                hours_angle = math.radians(360 / 12 * (current_time.hour % 12 - 3))
                
                minutes_angle = math.radians(360 / 60 * (current_time.minute - 15))
                
                seconds_angle = math.radians(360 / 60 * (current_time.second - 15))

                
                hour_hand_length = clock_radius * 0.5   
                
                minute_hand_length = clock_radius * 0.7 
                
                second_hand_length = clock_radius * 0.9 

              
                hour_hand_x = center_x + int(hour_hand_length * math.cos(
                    hours_angle)) 
              
                hour_hand_y = center_y + int(hour_hand_length * math.sin(
                    hours_angle)) 
              
                self.canvas.create_line(center_x, center_y, hour_hand_x, 
                hour_hand_y, fill="#333", width=6)   

              
                minute_hand_x = center_x + int(minute_hand_length * math.cos(
                    minutes_angle)) 
              
                minute_hand_y = center_y + int(minute_hand_length * math.sin(
                    minutes_angle)) 
              
                self.canvas.create_line(center_x, center_y, minute_hand_x, 
                minute_hand_y, fill="#3498db", width=4)   

              
                second_hand_x = center_x + int(second_hand_length * math.cos(
                    seconds_angle)) 
              
                second_hand_y = center_y + int(second_hand_length * math.sin(
                    seconds_angle)) 
              
                self.canvas.create_line(center_x, center_y, second_hand_x, 
                second_hand_y, fill="#e74c32", width=2)   

                
                self.root.after(1000, self.draw_clock)



if __name__ == "__main__":
    root = tk.Tk()
    app = AnalogClockApp(root)
    root.mainloop()      

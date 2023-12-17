import tkinter as tk
from tkinter import ttk
import random
import os
import cv2
import threading

class FullscreenVideoApp:
    def __init__(self, root, video_path):
        self.root = root
        self.root.attributes('-fullscreen', True)
        self.root.title("Кнопка и Видео")

        self.mouse_over_count = 0
        self.button_width = 200
        self.button_height = 50
        self.video_path = video_path

        self.create_button()

    def create_button(self):
        self.button = ttk.Button(self.root, text="Нажми на меня", command=self.button_click)
        self.button.place(x=0, y=0)
        self.button.bind("<Enter>", lambda event: self.randomize_button_position())

    def randomize_button_position(self):
        if self.mouse_over_count < 10:
            x = random.randint(0, self.root.winfo_screenwidth() - self.button_width)
            y = random.randint(0, self.root.winfo_screenheight() - self.button_height)
            self.button.place(x=x, y=y)
            self.mouse_over_count += 1
        else:
            self.root.after(1000, self.root.quit)  # Завершаем работу приложения через 1 секунду
            self.play_video()

    def button_click(self):
        self.root.destroy()  # Закрываем основное окно
        self.play_video()

    def play_video(self):
        cap = cv2.VideoCapture(self.video_path)

        while True:
            ret, frame = cap.read()
            if not ret:
                break

            cv2.namedWindow("Видео", cv2.WND_PROP_FULLSCREEN)
            cv2.setWindowProperty("Видео", cv2.WND_PROP_FULLSCREEN, cv2.WINDOW_FULLSCREEN)
            cv2.imshow("Видео", frame)

            if cv2.waitKey(25) & 0xFF == 27:  # Нажмите 'Esc', чтобы выйти
                break

        cap.release()
        cv2.destroyAllWindows()

if __name__ == "__main__":
    video_path = "video.mp4"
    root = tk.Tk()
    app = FullscreenVideoApp(root, video_path)
    root.mainloop()

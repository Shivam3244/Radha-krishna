import cv2
import numpy as np
import turtle
import os
import random
import math
import tkinter

# --- Load and Preprocess Image ---
script_dir = os.path.dirname(os.path.abspath(__file__))
image_path = os.path.join(script_dir, 'radha.jpg')
img = cv2.imread(image_path)

if img is None:
    print(f"Error: Could not load image at '{image_path}'")
    exit()

# Set canvas dimensions
width, height = 600, 600
img = cv2.resize(img, (width, height))

# Grayscale & Edge Detection
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
blur = cv2.GaussianBlur(gray, (5, 5), 0)
edges = cv2.Canny(blur, 40, 120)

# Find contours
contours, _ = cv2.findContours(edges, cv2.RETR_LIST, cv2.CHAIN_APPROX_NONE)

# Filter short noise contours & sort by length (draw outer/larger lines first)
valid_contours = [cnt for cnt in contours if len(cnt) >= 6]
valid_contours.sort(key=lambda c: len(c), reverse=True)

# --- 2. Color Palette & Feature Mapper ---
def get_janmashtami_color(x_px, y_px):
    """
    Map (x_px, y_px) image coordinates to divine Janmashtami color themes.
    x_px: 0 to 600 (left to right)
    y_px: 0 to 600 (top to bottom)
    """
    # Mor Pankh (Peacock Feather on Krishna's crown at top-center)
    if y_px < 120 and 200 <= x_px <= 340:
        feather_colors = [
            (0, 230, 255),    # Vibrant Cyan
            (0, 210, 140),    # Emerald Peacock Green
            (255, 215, 0),    # Bright Gold
            (30, 144, 255),   # Royal Blue
            (186, 85, 211)    # Medium Orchid
        ]
        return random.choice(feather_colors)
    
    # Bansuri (Flute around y: 130..190, x: 150..350)
    if 130 <= y_px <= 190 and 150 <= x_px <= 350:
        flute_colors = [
            (255, 215, 0),    # Bright Gold
            (255, 180, 40),   # Warm Amber
            (255, 235, 150)   # Light Gold Glow
        ]
        return random.choice(flute_colors)
    
    # Floor line / Base accents
    if y_px > 550:
        return (255, 200, 80)
    
    # Radha's Side (Right half) vs Krishna's Side (Left half)
    if x_px >= 310:
        # Radha's Divine Palette: Rose Gold, Crimson, Magenta, Warm Gold
        radha_colors = [
            (255, 105, 180),  # Hot Pink
            (255, 182, 193),  # Light Pink
            (255, 215, 0),    # Bright Gold
            (238, 130, 238),  # Violet
            (255, 160, 122)   # Light Salmon / Peach
        ]
        return random.choice(radha_colors)
    else:
        # Krishna's Divine Palette: Sky Cyan, Royal Blue, Deep Blue, Soft Violet
        krishna_colors = [
            (0, 215, 255),    # Bright Sky Cyan
            (65, 105, 225),   # Royal Blue
            (100, 200, 255),  # Soft Cyan Glow
            (138, 43, 226),   # Blue Violet
            (0, 191, 255)     # Deep Sky Blue
        ]
        return random.choice(krishna_colors)

# --- 3. Setup Turtle Window ---
screen = turtle.Screen()
screen.setup(width=850, height=850)
screen.bgcolor("#070B19")  # Deep Cosmic Midnight Blue
screen.title("✨ Shree Krishna Janmashtami - Radha Krishna Sketch ✨")
turtle.colormode(255)
screen.tracer(0)

# Pen Turtle
t = turtle.Turtle()
t.speed(0)
t.shape("circle")
t.shapesize(0.3, 0.3)
t.color("gold")
t.pensize(2)

# --- 4. Render Background Elements & Title ---
def draw_starry_background():
    star_turtle = turtle.Turtle()
    star_turtle.hideturtle()
    star_turtle.penup()
    star_turtle.speed(0)
    
    # Draw background stars
    for _ in range(80):
        x = random.randint(-400, 400)
        y = random.randint(-380, 380)
        # Avoid drawing directly over title area
        if y > 300:
            continue
        size = random.uniform(1, 3)
        star_turtle.goto(x, y)
        star_turtle.dot(size, random.choice(["#FFF8DC", "#E0FFFF", "#FFD700", "#B0E0E6"]))

def draw_festive_header():
    title_turtle = turtle.Turtle()
    title_turtle.hideturtle()
    title_turtle.penup()
    
    # Main Header
    title_turtle.goto(0, 350)
    title_turtle.color("#FFD700")  # Gold shadow/glow
    title_turtle.write("🌸 SHREE KRISHNA JANMASHTAMI 🌸", align="center", font=("Georgia", 22, "bold"))
    
    title_turtle.goto(0, 320)
    title_turtle.color("#00E5FF")  # Radiant Cyan
    title_turtle.write("✨ Radhe Radhe • Jai Shree Krishna ✨", align="center", font=("Georgia", 13, "italic"))

# Draw initial background & title
draw_starry_background()
draw_festive_header()
screen.update()

# Y-offset shift to center sketch below header
y_offset = -30

print("Drawing Shree Krishna Janmashtami Sketch...")

# --- 5. Main Sketch Loop with Error Protection ---
try:
    drawn_points = 0
    for cnt in valid_contours:
        t.penup()
        first_pt = cnt[0][0]
        x_px, y_px = first_pt[0], first_pt[1]
        
        # Determine themed color
        r, g, b = get_janmashtami_color(x_px, y_px)
        t.pencolor(r, g, b)
        
        # Convert OpenCV coords (0 to 600) to Turtle centered coords (-300 to 300)
        start_x = x_px - width // 2
        start_y = (height // 2 - y_px) + y_offset
        
        t.goto(start_x, start_y)
        t.pendown()
        
        for pt in cnt[1:]:
            px, py = pt[0][0], pt[0][1]
            x = px - width // 2
            y = (height // 2 - py) + y_offset
            t.goto(x, y)
            
            drawn_points += 1
            # Update screen periodically for smooth non-laggy animation
            if drawn_points % 12 == 0:
                screen.update()

    screen.update()
    t.hideturtle()
    
    # Festive Completion Message & Sparkle Shower
    celebration_turtle = turtle.Turtle()
    celebration_turtle.hideturtle()
    celebration_turtle.penup()
    celebration_turtle.goto(0, -360)
    celebration_turtle.color("#FFD700")
    celebration_turtle.write("✨ Divine Sketch Complete! Wishing You A Blessed Janmashtami ✨", align="center", font=("Georgia", 12, "bold"))
    
    # Sparkle explosion around Radha Krishna
    for _ in range(40):
        angle = random.uniform(0, 2 * math.pi)
        radius = random.uniform(50, 320)
        sx = radius * math.cos(angle)
        sy = radius * math.sin(angle) + y_offset
        celebration_turtle.goto(sx, sy)
        celebration_turtle.dot(random.randint(3, 7), random.choice(["#FFD700", "#00FFFF", "#FF69B4", "#7FFFD4"]))
        screen.update()
        
    print("Drawing Complete! Happy Janmashtami!")

except (turtle.Terminator, tkinter.TclError):
    print("Turtle window was closed by the user.")

try:
    turtle.done()
except (turtle.Terminator, tkinter.TclError):
    pass

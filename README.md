# 🌸 Shree Krishna Janmashtami — Radha Krishna Sketch 🌸

**✨ Radhe Radhe • Jai Shree Krishna ✨**

*A Python art project that transforms a photo into a glowing, hand-drawn Radha-Krishna sketch using edge detection and turtle graphics — wrapped in a festive Janmashtami theme.*

**Python 3.8+ • OpenCV • Turtle Graphics • MIT License**

---

## 🪈 About the Project

This script takes an image (`radha.jpg`) and reimagines it as a luminous, animated line sketch — drawn stroke by stroke on a cosmic midnight-blue canvas. It's built specifically for **Janmashtami**, using color themes inspired by:

- 🪶 **Mor Pankh** (Peacock Feather) — vibrant cyans, emeralds & gold near the crown
- 🎋 **Bansuri** (Flute) — warm gold and amber tones
- 💗 **Radha's Side** — rose gold, crimson, magenta & warm gold hues
- 💙 **Krishna's Side** — sky cyan, royal blue & soft violet hues
- ⭐ A **starry night sky background** with a festive glowing title
- 🎆 A **sparkle shower animation** on completion

The result is a slow-drawn, animated piece of generative art — perfect for sharing on Janmashtami!

---

## 🎨 How It Works

1. **Image Loading & Preprocessing** — Loads `radha.jpg`, resizes it to `600x600`, and converts it to grayscale.
2. **Edge Detection** — Applies Gaussian blur + **Canny edge detection** (via OpenCV) to extract the outlines of the image.
3. **Contour Extraction** — Finds and filters contours, sorting them so larger/outer lines are drawn first.
4. **Themed Coloring** — Maps each contour's position to a divine color palette (peacock feather, flute, Radha's side, Krishna's side, etc.).
5. **Turtle Animation** — Draws every contour live on screen using Python's `turtle` module, with a starry background and festive header text.
6. **Grand Finale** — Once drawing is complete, a sparkle burst animation celebrates the finished artwork with a Janmashtami blessing message.

---

## 📦 Requirements

- Python 3.8+
- [OpenCV](https://pypi.org/project/opencv-python/) (`opencv-python`)
- [NumPy](https://pypi.org/project/numpy/)
- `turtle` and `tkinter` (usually bundled with standard Python installations)

### Install dependencies

```bash
pip install opencv-python numpy
```

> 💡 On some Linux distributions, `tkinter` isn't installed by default. Install it via:
> ```bash
> sudo apt-get install python3-tk
> ```

---

## 🚀 Usage

1. Clone this repository:
   ```bash
   git clone https://github.com/mshivam017/janmashtami-edition.git
   cd janmashtami-edition
   ```

2. Place an image named **`radha.jpg`** in the same directory as the script.

3. Run the script:
   ```bash
   python radhakrishna.py
   ```

4. Sit back and watch the divine sketch come to life! 🎨✨

> ⚠️ Make sure `radha.jpg` exists in the script's directory — the program will exit with an error if the image can't be found.

---

## ⚙️ Customization

| What you want to change | Where to edit |
|---|---|
| Canvas size | `width, height = 600, 600` |
| Edge sensitivity | `cv2.Canny(blur, 40, 120)` thresholds |
| Color palettes | `get_janmashtami_color()` function |
| Background color | `screen.bgcolor("#070B19")` |
| Title text | `draw_festive_header()` function |
| Sparkle count/finale | The `for _ in range(40)` loop at the end |

---

## 🙏 Credits

Made with devotion for **Shree Krishna Janmashtami** 🪈💙

If you enjoyed this project, consider giving it a ⭐ on GitHub!

---

**✨ Wishing you a Blessed Janmashtami ✨**

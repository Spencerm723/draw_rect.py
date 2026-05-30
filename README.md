import sys
from picture import Picture
import stddraw

def scale(image, factor):
    new_width = int(image.width() * factor)
    new_height = int(image.height() * factor)

    new_image = Picture(new_width, new_height)

    for x in range(new_width):
        for y in range(new_height):
            orig_x = int(x / factor)
            orig_y = int(y / factor)
            new_image.set(x, y, image.get(orig_x, orig_y))

    return new_image

def draw_rectangle(image, x_frac, y_frac, width, height):
    center_x = int(x_frac * image.width())
    center_y = int(y_frac * image.height())

    top_left_x = center_x - width // 2
    top_left_y = center_y - height // 2

    stddraw.setCanvasSize(image.width(), image.height())
    stddraw.setXscale(0, image.width())
    stddraw.setYscale(0, image.height())
    stddraw.picture(image)
    stddraw.setPenColor(stddraw.RED)
    stddraw.rectangle(top_left_x, top_left_y, width, height)
    stddraw.show()

def main():
    if len(sys.argv) != 5:
        print("Usage: python draw_rect.py <image-file> <scale-factor> <x> <y>")
        return

    filename = sys.argv[1]
    scale_factor = float(sys.argv[2])
    x_frac = float(sys.argv[3])
    y_frac = float(sys.argv[4])

    image = Picture(filename)
    scaled = scale(image, scale_factor)
    draw_rectangle(scaled, x_frac, y_frac, image.width(), image.height())

main()

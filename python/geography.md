## Get Vincenty distance between points

Coordinate order is latitude, longitude
```
from geopy.distance import vincenty
print(vincenty((25.26, 12.45), (25.2645, 12.45)).m)
```

## Get aspect ratio for bounding box

Bounding box in lon, lat (lower-left, upper-right) order:

```
from geopy.distance import vincenty

def get_aspect_ratio(bbox, max_pixels):
    x1, y1, x2, y2 = bbox
    dist_x = (vincenty((y1, x1), (y1, x2)).m + vincenty((y1, x1), (y1, x2)).m) / 2
    dist_y = vincenty((y1, x1), (y2, x1)).m
    if dist_x > dist_y:
        return max_pixels, round(max_pixels * dist_y / dist_x)
    else:
        return round(max_pixels * dist_x / dist_y), max_pixels

```

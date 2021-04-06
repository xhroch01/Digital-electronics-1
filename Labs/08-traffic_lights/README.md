# 1

## State table

| **Input P** | 0 | 0 | 1 | 1 | 0 | 1 | 0 | 1 | 1 | 1 | 1 | 0 | 0 | 1 | 1 | 1 |
| :-- | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| **Clock** | ![1](IMAGES/sipka.PNG) | ![1](IMAGES/sipka.PNG) | ![1](IMAGES/sipka.PNG) | ![1](IMAGES/sipka.PNG) | ![1](IMAGES/sipka.PNG) | ![1](IMAGES/sipka.PNG) | ![1](IMAGES/sipka.PNG) | ![1](IMAGES/sipka.PNG) | ![1](IMAGES/sipka.PNG) | ![1](IMAGES/sipka.PNG) | ![1](IMAGES/sipka.PNG) | ![1](IMAGES/sipka.PNG) | ![1](IMAGES/sipka.PNG) | ![1](IMAGES/sipka.PNG) | ![1](IMAGES/sipka.PNG) | ![1](IMAGES/sipka.PNG) |
| **State** | A | A | B | C | C | D | A | B | C | D | B | B | B | C | D | B |
| **Output R** | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 1 | 0 |

### Figure with connection of RGB LEDs on Nexys A7 board and completed table with color settings.

![1](IMAGES/schema1.PNG)

| **RGB LED** | **Artix-7 pin names** | **Red** | **Yellow** | **Green** |
| :-: | :-: | :-: | :-: | :-: |
| LD16 | N15, M16, R12 | `1,0,0` | `1,1,0` | `0,1,0` |
| LD17 | N16, R11, G14 | `1,0,0` | `1,1,0` | `0,1,0` |

# 2

![1](IMAGES/kruh.PNG)

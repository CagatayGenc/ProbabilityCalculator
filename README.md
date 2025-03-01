```python
import copy
import random


class Hat:
    def __init__(self, **kwargs):
        self.contents = []
        for key, value in kwargs.items():
            for _ in range(value):
                self.contents.append(key)

    def draw(self, number):
        number = min(number, len(self.contents))
        drawn_items = []

        for _ in range(number):
            random_draw = random.randrange(len(self.contents))
            drawn_items.append(self.contents.pop(random_draw))

        return drawn_items


def experiment(hat, expected_balls, num_balls_drawn, num_experiments):
    count = 0

    for _ in range(num_experiments):
        another_hat = copy.deepcopy(hat)
        balls_drawn = another_hat.draw(num_balls_drawn)

        balls_req = 0
        for key, value in expected_balls.items():
            if balls_drawn.count(key) >= value:
                balls_req += 1

        if balls_req == len(expected_balls):
            count +=1

    return count / num_experiments
```

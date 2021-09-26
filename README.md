# MINECRAFT
its a game thats is popular for brgginers
from ursina import *
from ursina.prefabs.first_person_controller import FirstPersonController


app = Ursina()

grass_texture = load_texture("asset/grass.png")
sky_texture = load_texture("asset/sky.png")
wood_texture = load_texture("asset/wood.png")
people_texture = load_texture("asset/people.png")
flower_texture = load_texture("asset/flower.png")
tree_texture = load_texture("asset/tree.png")
current_texture = grass_texture

def update():
    global current_texture
    if held_keys['1']: current_texture = grass_texture
    if held_keys['2']: current_texture = wood_texture
    if held_keys['3']: current_texture = people_texture
    if held_keys['4']: current_texture = flower_texture
    if held_keys['5']: current_texture = tree_texture

class sky(Entity):
    def __init__(self):
        super().__init__(
            parent=scene,
            model = 'sphere',
            scale = '150',
            texture = sky_texture,
            double_sided = True
        )





class Voxel(Button):
    def __init__(self,position=(0,0,0), texture = grass_texture):
        super().__init__(
            parent = scene,
            model = 'cube',
            color = color.white,
            highlight_color = color.lime,
            texture = texture,
            position = position,
            origin_y = 0.5

        )


    def input(self, key):
         if self.hovered:
             if key == "left mouse down":
                 voxel = Voxel(position=self.position + mouse.normal, texture=current_texture)
             if key == 'right mouse down':
                 destroy(self)
for z in range(15):
    for x in range(15):
        voxel = Voxel((x,0,z))
player = FirstPersonController()
sky = Sky()

app.run()

import random

def generateMap(m: int, n: int, ground_water_ration = .2, water = '0', ground = '1' ):
    r = int(m*n*ground_water_ration+.5)
    newMap = [[water]*m for _ in range(n)]
    coord = [(i, j) for i in range(n) for j in range(m)]
    random.shuffle(coord)
    for i, j in coord[:r]:
        newMap[i][j] = ground
    return newMap

def save_map(map_s, path = 'new_map.txt'):
    with open(path, 'wt') as f:
        for row in map_s:
            f.write("".join(map(str, row)))
            f.write('\n')

def print_map(map_p):
    for row in map_p:
        print("".join(map(str, row)))
random.seed(10012)


def count_islands(map):
    x=len(map)-1
    y=len (map[1])-1
    coords=[[i, j] for i in range(map) for j in range(map[0])]
    contei= set()
    n=0

    for k in coords:
        if k not in contei:
            contei.append(k)
            
    return n

if __name__=="__main__":
    m1 = generateMap(5, 5, 0.3) # Exemplo
    print_map(m1)

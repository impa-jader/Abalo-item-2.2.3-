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


def count_islands(map):
    y=len(map)-1
    x=len (map[0])-1
    def around(k):
        around=[]
        direçoes=[(-1,0),(-1,1),(-1,-1),(0,1),(0,-1),(1,-1),(1,0),(1,1)]
        for d in direçoes:
            if (k[0]+d[0],k[1]+d)[0]>=0 and (k[0]+d[0],k[1]+d)[1]>=0 and (k[0]+d[0],k[1]+d)[0]<=x and (k[0]+d[0],k[1]+d)[1]<=y:
                X,Y= k[0]+d[0],k[1]+d
                around.append(map[Y][X])
        return around

    coords=[(i, j) for i in range(len(map[0])) for j in range(len(map))]
    contei= set()
    n=0
    def find_island(monte_de_coisas):
        for k in monte_de_coisas:
            Já_contei_esta_ilha=False
            monte_de_coisas.pop(k)
            X,Y= k
            if k not in contei:
                contei.add(k)
                if map[Y][X]==1:
                    for m in around(k):
                        Xi,Yi=m
                        if m in contei and map[Yi][Xi]==1:
                            Já_contei_esta_ilha= True
                    if Já_contei_esta_ilha==False:
                        nonlocal n
                        print('potato')
                        n+= 1
                    next=[]
                    next.append(j for j in around(k))
                    while next!=[]:
                            find_island(next)
        find_island(coords)                    
    return n

if __name__=="__main__":
    mapa = generateMap(5, 5, 0.3)
    print_map(mapa)
    print(f"Número de ilhas: {count_islands(mapa)}")

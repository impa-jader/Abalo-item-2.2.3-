# Questão 3

import random


def generateMap(m: int, n: int, ground_water_ration = .2, water = 0, ground = 1 ):
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
    contei= set()
    coords=[(i, j) for i in range(len(map[0])) for j in range(len(map))]
    n=0
    def surrounding(k,l=[]):
        direçoes=[(-1,0),(-1,1),(-1,-1),(0,1),(0,-1),(1,-1),(1,0),(1,1)]
        for d in direçoes:
            if (k[0]+d[0],k[1]+d[1])[0]>=0 and (k[0]+d[0],k[1]+d[1])[1]>=0 and (k[0]+d[0],k[1]+d[1])[0]<=x and (k[0]+d[0],k[1]+d[1])[1]<=y:
                X,Y= k[0]+d[0],k[1]+d[1]
                if (X,Y) not in contei:
                    l.append((k[0]+d[0],k[1]+d[1]))

    def see_island(p):
        if p not in contei:
            contei.add(p)
            l=[p]
            X,Y=p
            if map[Y][X]== 1:
                nonlocal n
                n+=1
                for k in l:
                    contei.add(k)
                    if map[k[1]][k[0]]==1:
                        surrounding(k,l)
    for p in coords:
        see_island(p)
    return n

# Questão 4 
# Utilizarei o codigo da 3 como base
def bigest_island_centro(map):
    y=len(map)-1
    x=len (map[0])-1
    islands=[]
    Mei=[] #Meior ilha
    contei= set()
    coords=[(i, j) for i in range(len(map[0])) for j in range(len(map))]
    def surrounding(k,l=[]):
        direçoes=[(-1,0),(-1,1),(-1,-1),(0,1),(0,-1),(1,-1),(1,0),(1,1)]
        for d in direçoes:
            if (k[0]+d[0],k[1]+d[1])[0]>=0 and (k[0]+d[0],k[1]+d[1])[1]>=0 and (k[0]+d[0],k[1]+d[1])[0]<=x and (k[0]+d[0],k[1]+d[1])[1]<=y:
                X,Y= k[0]+d[0],k[1]+d[1]
                if (X,Y) not in contei:
                    l.append((k[0]+d[0],k[1]+d[1]))

    def see_island_coords(p):
        if p not in contei:
            contei.add(p)
            l=[p]
            X,Y=p
            ilha_terra=[]
            if map[Y][X]== 1:
                for k in l:
                    contei.add(k)
                    if map[k[1]][k[0]]==1:
                        ilha_terra.append(k)
                        surrounding(k,l)
            return ilha_terra
            
            
    for p in coords:
        X,Y=p
        if p not in contei and map[Y][X]== 1: # Talvez algumas condições estejam redundantes com see_island_coords, mas tava bugando e o jeito de corrigir foi este. Deve dar apaga alguma das condições redundantes mas não farei isto agora.
            islands.append(see_island_coords(p))
    #print(islands)
    for i in islands:
        if len(i)>len(Mei):
            Mei=i
    # Assim, Mei é o conjunto de coordenadas da Meior ilha. Para calcular o centro, farei a média das coordenadas e arredondarei
    Xc=0
    Yc=0
    for j in Mei:
        Xc+=j[0]/len(Mei)
        Yc+=j[1]/len(Mei)
 
    return (round(Xc),round(Yc))

def smalest_island_centro(map):
    y=len(map)-1
    x=len (map[0])-1
    islands=[]
    Mei=[] #menor ilha
    contei= set()
    coords=[(i, j) for i in range(len(map[0])) for j in range(len(map))]
    def surrounding(k,l=[]):
        direçoes=[(-1,0),(-1,1),(-1,-1),(0,1),(0,-1),(1,-1),(1,0),(1,1)]
        for d in direçoes:
            if (k[0]+d[0],k[1]+d[1])[0]>=0 and (k[0]+d[0],k[1]+d[1])[1]>=0 and (k[0]+d[0],k[1]+d[1])[0]<=x and (k[0]+d[0],k[1]+d[1])[1]<=y:
                X,Y= k[0]+d[0],k[1]+d[1]
                if (X,Y) not in contei:
                    l.append((k[0]+d[0],k[1]+d[1]))

    def see_island_coords(p):
        if p not in contei:
            contei.add(p)
            l=[p]
            X,Y=p
            ilha_terra=[]
            if map[Y][X]== 1:
                for k in l:
                    contei.add(k)
                    if map[k[1]][k[0]]==1:
                        ilha_terra.append(k)
                        surrounding(k,l)
            return ilha_terra
            
            
    for p in coords:
        X,Y=p
        if p not in contei and map[Y][X]== 1: # Talvez algumas condições estejam redundantes com see_island_coords, mas tava bugando e o jeito de corrigir foi este. Deve dar apaga alguma das condições redundantes mas não farei isto agora.
            islands.append(see_island_coords(p))
    print(islands)
    for i in islands:
        if len(i)<len(Mei):
            Mei=i
    # Assim, Mei é o conjunto de coordenadas da menor ilha. Para calcular o centro, farei a média das coordenadas e arredondarei
    Xc=0
    Yc=0
    for j in Mei:
        Xc+=j[0]/len(Mei)
        Yc+=j[1]/len(Mei)
 
    return (round(Xc),round(Yc))

# Questão 5
def tem_lago(map):
    coords=[(i, j) for i in range(len(map[0])) for j in range(len(map))]
    for i in coords:
        Visinhos=0
        Visinhos_terra=0
        X,Y= i
        direçoes=[(-1,0),(0,1),(0,-1),(1,0)]
        if map[Y][X]==0:
            for d in direçoes:
                if X+d[0]>=0 and Y+d[1]>=0 and X+d[0]<len(map[0]) and Y+d[1]<len(map):
                    Visinhos+=1
                    if map[Y+d[1]][X+d[0]]==1:
                        Visinhos_terra+=1
            if Visinhos==Visinhos_terra:
                return True
    return False


if __name__ == "__Mein__":
    mapa = generateMap(5, 5, 0.3)  
    print_map(mapa)  
    print(f"Número de ilhas: {count_islands(mapa)}")  
    #save_map(mapa, "new_map.txt")
    print(tem_lago(mapa))
    print(f"Centro da Meior ilha: {bigest_island_centro(mapa)}")

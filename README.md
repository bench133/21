# 21
code5
from math import dist
data = []
# Для А/Б
for s in open('3920.txt'):
    x, y = [float(d) for d in s.replace(',', '.').split()]
    data.append([x, y])
 
rast = 1
clusters = []
while data:
    cl = [data.pop()]
    for p in cl:
        sosed = [p1 for p1 in data if dist(p, p1) < rast]
        for p1 in sosed:
            cl.append(p1)
            data.remove(p1)
    clusters.append(cl)
 
#print(*[len(cl) for cl in clusters]) # - проверяет кол-во кластеров
# 2 кластера для файла A и 3 для файла B
# В случае противоречия меняем rast - это значение (Для A - rast = 2, для B - rast = 1)
 
def centroid(cl):
    m = []
    for p in cl:
        s = 0
        for p1 in cl:
            s += dist(p, p1)
        m.append([s, p])
    return min(m)[1]
 
cen = [centroid(cl) for cl in clusters]
px = abs(sum(x for x, y in cen))/len(cen)
py = abs(sum(y for x, y in cen))/len(cen)
 
print(int(px*10000), int(py*10000))

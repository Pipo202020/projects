# projects for FX I use Calculus to forecast next day Stock market movement. This is a module to calculate first and second derivate of day previous curve 



import numpy as np

# Cargar los datos desde el archivo polynomial.csv ignorando la primera columna
data = np.loadtxt("Funcion06-03-2023.csv", delimiter=",", usecols=range(1,13))
print("Forma del arreglo de coeficientes:", data.shape)

def polynomial_derivatives(coeffs):
    # Calcular la primera y segunda derivada de la función polinómica para un conjunto de coeficientes dados
    dy = np.polyder(coeffs)
    d2y = np.polyder(dy)
    
    return dy, d2y

# Inicializar las sumas de las derivadas
sum_dy = np.zeros(data.shape[0])
sum_d2y = np.zeros(data.shape[0])

# Iterar sobre todas las funciones y calcular las derivadas para cada una de ellas
for i in range(data.shape[0]):
    coeffs = data[i]
    dy, d2y = polynomial_derivatives(coeffs)
    
    # Calcular la suma de las primeras y segundas derivadas para cada función
    sum_dy[i] = np.sum(dy)
    sum_d2y[i] = np.sum(d2y)
    
    # Imprimir las funciones que son 0
    if np.all(dy == 0):
        print("La función polinómica", i+1, "tiene primera derivada igual a 0")
    if np.all(d2y == 0):
        print("La función polinómica", i+1, "tiene segunda derivada igual a 0")
    
    # Imprimir las derivadas para esta función
    print("Función polinómica", i+1)
    print("Primera derivada:\n", dy)
    print("Segunda derivada:\n", d2y)
    print()

# Imprimir las sumas de las derivadas
print("Suma de la primera derivada para todas las funciones:", np.sum(sum_dy))
print("Suma de la segunda derivada para todas las funciones:", np.sum(sum_d2y))


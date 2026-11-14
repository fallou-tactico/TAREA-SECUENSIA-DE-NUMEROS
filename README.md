import time

def encontrar_collatz_mas_largo(limite):
    # Diccionario (caché) para guardar la longitud de secuencias ya conocidas.
    # Caso base: el número 1 tiene una cadena de longitud 1.
    cache = {1: 1}
    
    max_longitud = 0
    mejor_inicio = 0

    for inicio in range(1, limite):
        n = inicio
        pasos = 0
        
        # Avanzamos en la secuencia hasta encontrar un número ya calculado en el caché
        while n not in cache:
            if n % 2 == 0:
                n = n // 2
            else:
                n = 3 * n + 1
            pasos += 1
        
        # La longitud total es los pasos nuevos dados + la longitud guardada en caché
        longitud_total = pasos + cache[n]
        cache[inicio] = longitud_total
        
        # Actualizamos el récord si encontramos una cadena más larga
        if longitud_total > max_longitud:
            max_longitud = longitud_total
            mejor_inicio = inicio

    return mejor_inicio, max_longitud

if __name__ == "__main__":
    LIMITE = 1_000_000
    
    tiempo_inicio = time.time()
    numero_ganador, longitud = encontrar_collatz_mas_largo(LIMITE)
    tiempo_fin = time.time()
    
    print(f"Número inicial con la cadena más larga (< {LIMITE:,}): {numero_ganador}")
    print(f"Cantidad de términos en la cadena: {longitud}")
    print(f"Tiempo de ejecución: {tiempo_fin - tiempo_inicio:.4f} segundos")
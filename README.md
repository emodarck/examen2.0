# examen2.0
2.0

products = {
    "R475HD": ["HP", "15.6", "8GB", "DD", "1TB", "Intel Core i5", "Nvidia GTX1050", 978],
    "2175HD": ["Lenovo", "14", "4GB", "SSD", "512GB", "Intel Core i5", "Nvidia GTX1050", 650],
    "JjfHD": ["Asus", "14", "16GB", "SSD", "256GB", "Intel Core i7", "Nvidia RTX2080Ti", 1800],
    "fgdxFHD": ["HP", "15.6", "8GB", "DD", "1TB", "Intel Core i3", "Integrada", 550],
    "GF75HD": ["Asus", "15.6", "8GB", "DD", "1TB", "Intel Core i7", "Nvidia GTX1050", 1100],
    "123FHD": ["Lenovo", "14", "6GB", "DD", "1TB", "AMD Ryzen 5", "Integrada", 700],
    "342FHD": ["Lenovo", "15.6", "8GB", "DD", "1TB", "AMD Ryzen 7", "Nvidia GTX1050", 900],
    "UWU131HD": ["Dell", "15.6", "8GB", "DD", "1TB", "AMD Ryzen 3", "Nvidia GTX1050", 634],
}

stock = {
    "R475HD": True,
    "2175HD": True,
    "JjfHD": True,
    "fgdxFHD": True,
    "GF75HD": True,
    "123FHD": True,
    "342FHD": True,
    "UWU131HD": True,
}

def stock_marca(brand):
    count = 0
    brand_lower = brand.lower()
    for model, details in products.items():
        if details[0].lower() == brand_lower and stock.get(model, False):
            count += 1
    return count

def busqueda_por_precio(min_price, max_price):
    found_notebooks = []
    for model, details in products.items():
        price = details[-1]
        if min_price <= price <= max_price and stock.get(model, False):
            found_notebooks.append(model)
    return found_notebooks

def actualizar_precio(model_to_update, new_price):
    for model, details in products.items():
        if model.lower() == model_to_update.lower():
            details[-1] = new_price
            return True
    return False

def handle_stock_marca():
    brand = input("Ingrese la marca a consultar: ")
    stock_count = stock_marca(brand)
    print(f"El stock disponible para {brand} es: {stock_count}")

def handle_busqueda_por_precio():
    while True:
        try:
            min_price = int(input("Ingrese el precio mínimo: "))
            break
        except ValueError:
            print("Tiene que ser un número entero para el precio mínimo.")
    while True:
        try:
            max_price = int(input("Ingrese el precio máximo: "))
            if max_price < min_price:
                print("El precio máximo no puede ser más chico que el mínimo. Intente de nuevo.")
            else:
                break
        except ValueError:
            print("Tiene que ser un número entero para el precio máximo.")

    results = busqueda_por_precio(min_price, max_price)
    if results:
        print(f"Los notebooks entre ${min_price} y ${max_price} son: {', '.join(results)}")
    else:
        print("No pillamos notebooks en ese rango de precios o no hay stock.")

def handle_actualizar_precio():
    model = input("Ingrese el modelo del notebook a actualizar: ")
    while True:
        try:
            new_price = int(input(f"Ingrese el nuevo precio para {model}: "))
            break
        except ValueError:
            print("Ojo. Tiene que ser un número entero para el precio.")

    if actualizar_precio(model, new_price):
        print(f"El precio de {model} quedó actualizado a ${new_price}.")
    else:
        print(f"El modelo '{model}' no existe o no se pudo actualizar el precio a compar.")

def handle_salir():
    print("Gracias por usar el sistema. Chao que te vaya bien.")
    return False 

def main_menu():
    
    menu_options = {
        1: handle_stock_marca,
        2: handle_busqueda_por_precio,
        3: handle_actualizar_precio,
        4: handle_salir
    }

    while True:
        print("\n*** MENÚ PRINCIPAL ***")
        print("1. Consultar stock por marca")
        print("2. Buscar por rango de precio")
        print("3. Actualizar precio de un modelo")
        print("4. Salir")

        try:
            option = int(input("\nIngrese su opción: "))
            
          
            action = menu_options.get(option)
            if action:
                if action() is False: 
                    break
            else:
                print("Esa opción no existe. Elija un número del 1 al 4, por favor.")

        except ValueError:
            print("Algo raro ingresó. Ponga un número para elegir la opción.")

if __name__ == "__main__":
    main_menu()

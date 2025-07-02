#Sistema Bancario
#Guardar información en un archivo de texto, cada línea tiene: numero de cuenta, DNI, correo electrónico y saldo.
#cliente derecho a X depositos
#Solicitar número de cuenta, DNI Y MONTO A DEPOSITAR PARA PROCESAR deposito, incrementando el saldo del cliente
#copiar ruta de archivo
#Autora: Solange M.

itf_rate = 0.00005
comision_retiro = 6.5

def cargar_datos():
    clientes = []
    ruta = "C:\\Users\\tecnoadmin\\Downloads\\P1_clientes.txt"
    with open(ruta, "r") as archivo:
        for linea in archivo:
            cuenta, dni, nombre, correo, saldo = linea.strip().split(",")
            clientes.append([
                cuenta, dni, nombre, correo, float(saldo)
            ])
    return clientes

def guardar_datos(clientes):
    ruta = "C:\\Users\\tecnoadmin\\Downloads\\P1_clientes.txt"
    with open(ruta, "w") as archivo:
        for cliente in clientes:
            archivo.write(",".join([cliente[0], cliente[1], cliente[2], cliente[3], f"{cliente[4]:.2f}"]) + "\n")

def buscar_cliente(clientes, cuenta, dni):
    for i, cliente in enumerate(clientes):
        if cliente[0] == cuenta and cliente[1] == dni:
            return i
    return -1

def hacer_deposito(clientes):
    cuenta = input("Cuenta: ")
    dni = input("DNI: ")
    monto = float(input("Monto a depositar: "))
    pos = buscar_cliente(clientes, cuenta, dni)
    if pos == -1:
        print("Cliente no encontrado.")
        return

    if monto >= 1000:
        monto -= monto * itf_rate
    clientes[pos][4] += monto
    print("Depósito realizado. Nuevo saldo:", round(clientes[pos][4], 2))

def hacer_retiro(clientes, retiros):
    cuenta = input("Cuenta: ")
    dni = input("DNI: ")
    pos = buscar_cliente(clientes, cuenta, dni)
    if pos == -1:
        print("Cliente no encontrado.")
        return

    if cuenta not in retiros:
        retiros[cuenta] = 0

    valido = False
    while not valido:
        monto = float(input("Monto a retirar: "))
        total = monto
        if retiros[cuenta] >= 2:
            total += comision_retiro

        if clientes[pos][4] >= total:
            clientes[pos][4] -= total
            retiros[cuenta] += 1
            print("Retiro realizado. Nuevo saldo:", round(clientes[pos][4], 2))
            valido = True

        else:
            print("Saldo insuficiente. Por favor, ingrese otro monto.")

def hacer_transferencia(clientes):
    cuenta_origen = input("Cuenta origen: ")
    dni_origen = input("DNI origen: ")
    cuenta_destino = input("Cuenta destino: ")
    dni_destino = input("DNI destino: ")
    monto = float(input("Monto a transferir: "))

    pos_origen = buscar_cliente(clientes, cuenta_origen, dni_origen)
    pos_destino = buscar_cliente(clientes, cuenta_destino, dni_destino)

    if pos_origen == -1 or pos_destino == -1:
        print("Cuenta o DNI incorrectos.")
        return

    total_origen = monto + monto * itf_rate
    total_destino_itf = monto * itf_rate

    if clientes[pos_origen][4] >= total_origen and clientes[pos_destino][4] >= total_destino_itf:
        clientes[pos_origen][4] -= total_origen
        clientes[pos_destino][4] += monto
        clientes[pos_destino][4] -= total_destino_itf
        print("Transferencia realizada.")
        print("Nuevo saldo origen:", round(clientes[pos_origen][4], 2))
        print("Nuevo saldo destino:", round(clientes[pos_destino][4], 2))

    else:
        print("Saldo insuficiente en alguna de las cuentas.")

def main():
    clientes = cargar_datos()
    retiros = {}

    while True:
        print("\n-- MENÚ --")
        print("1. Depósito")
        print("2. Retiro")
        print("3. Transferencia")
        print("4. Salir")
        opcion = input("Elige una opción: ").strip()

        if opcion not in ["1", "2", "3", "4"]:
            print("Opción inválida.")

        else:
            if opcion == "1":
                hacer_deposito(clientes)
            elif opcion == "2":
                hacer_retiro(clientes, retiros)
            elif opcion == "3":
                hacer_transferencia(clientes)
            elif opcion == "4":
                guardar_datos(clientes)
                print("Gracias por usar este Sistema Bancario.")
                return
if __name__ == "__main__":
    main()

#include <iostream> // Solo usamos esta librería

using namespace std;

int main() {
    int opcion;
    bool continuar = true;

    while (continuar) {
        // Menú de opciones
        cout << "Seleccione la operación que desea realizar:" << endl;
        cout << "1. Conversión de Longitud (Metros a Centímetros)" << endl;
        cout << "2. Conversión de Peso (Kilogramos a Gramos)" << endl;
        cout << "3. Cálculo del Área de un Círculo" << endl;
        cout << "4. Cálculo del Volumen de una Esfera" << endl;
        cout << "5. Salir" << endl;
        cout << "Opción: ";
        cin >> opcion;

        // Validación de entrada
        if(cin.fail() || opcion < 1 || opcion > 5) {
            cout << "Opción inválida. Por favor, ingrese un número entre 1 y 5." << endl;
            cin.clear(); // Limpia el error
            cin.ignore(10000, '\n'); // Limpia el buffer
            continue;
        }

        // Variables para los cálculos
        float metros, centimetros, kilogramos, gramos, radio, area, volumen;

        switch (opcion) {
            case 1: // Conversión de Longitud
                cout << "Ingresa una distancia en metros: ";
                cin >> metros;

                // Validar que la entrada sea positiva
                if (metros < 0) {
                    cout << "La distancia debe ser un número positivo." << endl;
                    break;
                }

                centimetros = metros * 100;
                cout << metros << " metros son " << centimetros << " centímetros." << endl;
                break;

            case 2: // Conversión de Peso
                cout << "Ingresa un peso en kilogramos: ";
                cin >> kilogramos;

                // Validar que la entrada sea positiva
                if (kilogramos < 0) {
                    cout << "El peso debe ser un número positivo." << endl;
                    break;
                }

                gramos = kilogramos * 1000;
                cout << kilogramos << " kilogramos son " << gramos << " gramos." << endl;
                break;

            case 3: // Cálculo de área del círculo
                cout << "Ingresa el radio del círculo en metros: ";
                cin >> radio;

                // Validar que el radio sea positivo
                if (radio < 0) {
                    cout << "El radio debe ser un número positivo." << endl;
                    break;
                }

                // Cálculo del área sin usar M_PI, usamos el valor de pi manualmente
                area = 3.14159 * radio * radio;
                cout << "El área del círculo con radio " << radio << " metros es " << area << " metros cuadrados." << endl;
                break;

            case 4: // Cálculo del volumen de la esfera
                cout << "Ingresa el radio de la esfera en metros: ";
                cin >> radio;

                // Validar que el radio sea positivo
                if (radio < 0) {
                    cout << "El radio debe ser un número positivo." << endl;
                    break;
                }

                // Cálculo del volumen sin usar M_PI, usamos el valor de pi manualmente
                volumen = (4.0 / 3.0) * 3.14159 * radio * radio * radio;
                cout << "El volumen de la esfera con radio " << radio << " metros es " << volumen << " metros cúbicos." << endl;
                break;

            case 5: // Salir
                cout << "Gracias por usar el programa. ¡Hasta luego!" << endl;
                continuar = false;
                break;

            default:
                cout << "Opción inválida. Por favor, seleccione un número entre 1 y 5." << endl;
                break;
        }

        cout << endl; // Separador para una mejor 


        
    }

    return 0;
}

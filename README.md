Proyecto: Sistema de Gestión de Plantas Medicinales

Este proyecto es un sistema interactivo de consola para gestionar información sobre plantas medicinales. Permite agregar, eliminar, visualizar y almacenar información sobre plantas medicinales y sus propiedades, usos, y preparación. También permite asociar plantas a síntomas y guardar los datos en archivos de texto.
 Características
- Agregar y eliminar plantas medicinales.
- Ver información sobre plantas y sus propiedades.
- Asociar plantas con síntomas.
- Guardar la información de las plantas en archivos de texto.
- Guardar la información de las plantas agrupadas por síntomas en archivos de texto.
 Instrucciones de instalación

Este proyecto está escrito en C++ y utiliza bibliotecas estándar, por lo que no requiere instalaciones adicionales.

1. Asegúrate de tener un compilador de C++ instalado (por ejemplo, `g++`).
   
   En Linux, puedes instalarlo con:
   ```bash
   sudo apt-get install g++
En Windows, puedes usar MinGW o instalar un IDE como Code::Blocks o Visual Studio que incluya un compilador de C++.

Descarga el código fuente del proyecto en tu máquina local.

Compila el código fuente. Si estás usando g++, puedes compilarlo con el siguiente comando:

bash
Copiar
g++ -o plantas_medicinales plantas_medicinales.cpp
Ejecuta el programa:

bash
Copiar
./plantas_medicinales
Instrucciones de uso
Al ejecutar el programa, se mostrará un menú con las siguientes opciones:

Ver información sobre una planta específica.
Agregar o eliminar una planta.
Ver plantas recomendadas para un síntoma específico.
Guardar la información de las plantas en un archivo de texto.
Guardar las plantas agrupadas por síntomas en un archivo de texto.
Selecciona una opción introduciendo el número correspondiente.

El programa continuará ejecutándose hasta que elijas salir.

#include <iostream>
#include <string>
#include <vector>
#include <map>
#include <limits>
#include <algorithm>
#include <fstream>

using namespace std;

// Estructura que representa una planta medicinal
struct PlantaMedicinal {
    string nombre;       // Nombre de la planta
    string propiedades;  // Propiedades medicinales de la planta
    string usos;         // Usos de la planta en la medicina
    string preparacion;  // Preparación de la planta para su uso
};

// Estructura para representar una opción en el menú
struct OpcionMenu {
    int id;              // Identificador único de la opción
    string descripcion;  // Descripción de la opción en el menú
};

// Estructura para representar un síntoma
struct Sintoma {
    int id;              // Identificador único del síntoma
    string descripcion;  // Descripción del síntoma
};

// Función que muestra la información de una planta medicinal
void mostrarInformacion(const PlantaMedicinal& planta) {
    cout << "Nombre: " << planta.nombre << endl;
    cout << "Propiedades: " << planta.propiedades << endl;
    cout << "Usos: " << planta.usos << endl;
    cout << "Preparacion: " << planta.preparacion << endl;
    cout << endl;
}

// Función que muestra el menú de opciones disponibles
void mostrarMenu(const vector<OpcionMenu>& opciones) {
    cout << "Seleccione una opcion:" << endl;
    for (const auto& opcion : opciones) {
        cout << opcion.id << ". " << opcion.descripcion << endl;
    }
    cout << "Opcion: ";
}

// Función que muestra los síntomas disponibles
void mostrarSintomas(const vector<Sintoma>& sintomas) {
    cout << "Seleccione el sintoma que desea tratar:" << endl;
    for (const auto& sintoma : sintomas) {
        cout << sintoma.id << ". " << sintoma.descripcion << endl;
    }
    cout << "Opcion: ";
}

// Función que obtiene una opción válida del usuario dentro de un rango
int obtenerOpcion(int min, int max) {
    int opcion;
    // Asegura que la opción esté dentro del rango válido
    while (!(cin >> opcion) || opcion < min || opcion > max) {
        cout << "Opcion invalida. Intente de nuevo: ";
        cin.clear(); // Limpia el estado de error
        cin.ignore(numeric_limits<streamsize>::max(), '\n'); // Ignora la entrada incorrecta
    }
    return opcion;
}

// Función que permite agregar una nueva planta medicinal
void agregarPlanta(vector<PlantaMedicinal>& plantas) {
    PlantaMedicinal planta;
    cout << "Ingrese el nombre de la planta medicinal: ";
    cin.ignore(); // Ignora el salto de línea anterior
    getline(cin, planta.nombre); // Lee el nombre de la planta
    cout << "Ingrese las propiedades de la planta medicinal: ";
    getline(cin, planta.propiedades); // Lee las propiedades
    cout << "Ingrese los usos de la planta medicinal: ";
    getline(cin, planta.usos); // Lee los usos
    cout << "Ingrese el procedimiento de preparacion: ";
    getline(cin, planta.preparacion); // Lee el método de preparación
    plantas.push_back(planta); // Agrega la nueva planta al vector
    cout << "Planta medicinal agregada con exito." << endl;
}

// Función que permite eliminar una planta medicinal por su nombre
void eliminarPlanta(vector<PlantaMedicinal>& plantas) {
    string nombrePlanta;
    cout << "Ingrese el nombre de la planta medicinal que desea eliminar: ";
    cin.ignore(); // Ignora el salto de línea anterior
    getline(cin, nombrePlanta); // Lee el nombre de la planta a eliminar

    // Busca la planta en el vector y la elimina si la encuentra
    auto it = find_if(plantas.begin(), plantas.end(), [&](const PlantaMedicinal& p) {
        return p.nombre == nombrePlanta;
    });

    if (it != plantas.end()) {
        plantas.erase(it); // Elimina la planta del vector
        cout << "Planta medicinal eliminada con exito." << endl;
    } else {
        cout << "Planta medicinal no encontrada." << endl;
    }
}

// Función que muestra las plantas recomendadas para un síntoma dado
void mostrarPlantasPorSintoma(int sintoma, const map<int, vector<PlantaMedicinal>>& plantasPorSintoma) {
    auto it = plantasPorSintoma.find(sintoma); // Busca las plantas asociadas al síntoma
    if (it != plantasPorSintoma.end()) {
        cout << "\nPlantas recomendadas para este sintoma:\n";
        for (const auto& planta : it->second) {
            mostrarInformacion(planta); // Muestra la información de cada planta
        }
    } else {
        cout << "No se encontraron plantas para este sintoma.\n";
    }
}

// Función que guarda la lista de plantas medicinales en un archivo de texto
void guardarPlantasEnArchivo(const vector<PlantaMedicinal>& plantas) {
    ofstream archivo("plantas_medicinales.txt"); // Abre el archivo para escribir
    if (archivo.is_open()) {
        // Escribe la información de cada planta en el archivo
        for (const auto& planta : plantas) {
            archivo << "Nombre: " << planta.nombre << endl;
            archivo << "Propiedades: " << planta.propiedades << endl;
            archivo << "Usos: " << planta.usos << endl;
            archivo << "Preparacion: " << planta.preparacion << endl;
            archivo << "----------------------------" << endl;
        }
        archivo.close(); // Cierra el archivo
        cout << "Plantas medicinales guardadas exitosamente en plantas_medicinales.txt" << endl;
    } else {
        cout << "Error al abrir el archivo para guardar las plantas." << endl;
    }
}

// Función que guarda las plantas agrupadas por síntoma en un archivo de texto
void guardarPlantasPorSintomaEnArchivo(const map<int, vector<PlantaMedicinal>>& plantasPorSintoma) {
    ofstream archivo("plantas_por_sintoma.txt"); // Abre el archivo para escribir
    if (archivo.is_open()) {
        // Escribe las plantas agrupadas por síntoma en el archivo
        for (const auto& sintoma : plantasPorSintoma) {
            archivo << "Sintoma " << sintoma.first << ":" << endl;
            for (const auto& planta : sintoma.second) {
                archivo << "  - " << planta.nombre << endl;
            }
            archivo << "----------------------------" << endl;
        }
        archivo.close(); // Cierra el archivo
        cout << "Plantas por sintoma guardadas exitosamente en plantas_por_sintoma.txt" << endl;
    } else {
        cout << "Error al abrir el archivo para guardar las plantas por sintoma." << endl;
    }
}

// Función principal que gestiona el menú de opciones y el flujo del programa
int main() {
    vector<PlantaMedicinal> plantas; // Contenedor de plantas medicinales
    map<int, vector<PlantaMedicinal>> plantasPorSintoma; // Mapa que relaciona síntomas con plantas

    // Inicializa algunas plantas medicinales de ejemplo
    plantas.push_back({"Maca", "Aumenta la energia y la resistencia", "Usada para mejorar la libido", "Se consume en polvo o en capsulas"});
    plantas.push_back({"Aloe Vera", "Propiedades antiinflamatorias y cicatrizantes", "Usado para quemaduras y heridas", "Se aplica directamente sobre la piel"});
    plantas.push_back({"Huacatay", "Antibacteriano y antiinflamatorio", "Usado para problemas digestivos", "Se prepara en infusion"});
    plantas.push_back({"Una de Gato", "Fortalece el sistema inmunologico", "Usado para infecciones", "Se consume en te"});
    plantas.push_back({"Chanca Piedra", "Ayuda a disolver calculos renales", "Usado para problemas urinarios", "Se prepara en infusion"});

    // Asocia las plantas a los síntomas correspondientes
    plantasPorSintoma[1] = {plantas[0], plantas[1]};
    plantasPorSintoma[2] = {plantas[1]};
    plantasPorSintoma[3] = {plantas[2], plantas[3]};
    plantasPorSintoma[4] = {plantas[3]};
    plantasPorSintoma[5] = {plantas[4]};

    // Opciones del menú
    vector<OpcionMenu> opcionesMenu = {
        {1, "Maca"}, {2, "Aloe Vera"}, {3, "Huacatay"}, {4, "Una de Gato"}, {5, "Chanca Piedra"},
        {6, "Agregar planta medicinal"}, {7, "Eliminar planta medicinal"}, {8, "Seleccionar sintoma"},
        {9, "Guardar plantas en archivo"}, {10, "Guardar plantas por sintoma en archivo"}, {11, "Salir"}
    };

    // Lista de síntomas
    vector<Sintoma> sintomas = {
        {1, "Cansancio y falta de energia"}, {2, "Problemas de piel (quemaduras, heridas)"},
        {3, "Infecciones y bacterias"}, {4, "Dolencias del sistema inmunologico"},
        {5, "Problemas urinarios y calculos renales"}
    };

    int opcion;
    do {
        mostrarMenu(opcionesMenu); // Muestra el menú
        opcion = obtenerOpcion(1, opcionesMenu.size()); // Obtiene la opción seleccionada por el usuario

        switch (opcion) {
            case 1: case 2: case 3: case 4: case 5:
                mostrarInformacion(plantas[opcion - 1]); // Muestra la información de la planta seleccionada
                break;
            case 6:
                agregarPlanta(plantas); // Agrega una nueva planta
                break;
            case 7:
                eliminarPlanta(plantas); // Elimina una planta existente
                break;
            case 8: {
                mostrarSintomas(sintomas); // Muestra los síntomas disponibles
                int sintomaSeleccionado = obtenerOpcion(1, sintomas.size());
                mostrarPlantasPorSintoma(sintomaSeleccionado, plantasPorSintoma); // Muestra las plantas asociadas al síntoma seleccionado
                break;
            }
            case 9:
                guardarPlantasEnArchivo(plantas); // Guarda las plantas en un archivo
                break;
            case 10:
                guardarPlantasPorSintomaEnArchivo(plantasPorSintoma); // Guarda las plantas por síntoma en un archivo
                break;
            case 11:
                cout << "Saliendo del programa..." << endl; // Sale del programa
                break;
        }
    } while (opcion != 11); // Repite el ciclo hasta que el usuario elija salir

    return 0;
}

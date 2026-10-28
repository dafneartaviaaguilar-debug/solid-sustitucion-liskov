# Principio de Sustitución de Liskov
Proyecto en C++ que demuestra el tercer principio SOLID: **Liskov Substitution Principle**.

## ¿Qué dice el principio?

> Una clase hija debe poder **sustituir a su clase padre** sin que el programa deje de funcionar o cambie su comportamiento esperado.

## ¿Cómo se implementa en este proyecto?

La clase base `Producto` tiene un método `ConvertirPrecio()` que calcula el precio final usando el método virtual `AplicarDescuento()`. Cada clase hija redefine (`override`) **solo** el descuento, manteniendo el mismo significado y la misma firma:

| Clase | Descuento | Cálculo |
|-------|-----------|---------|
| `Fisico` | 30 % | `getPrecio() * 0.30` |
| `Digital` | 12 % | `getPrecio() * 0.12` |

### Código clave

```cpp
// Producto.cpp -> funciona igual con cualquier hijo
double Producto::ConvertirPrecio() {
    double Preciofinal = Precio - AplicarDescuento();
    return Preciofinal;
}

// Fisico.cpp
double Fisico::AplicarDescuento() {
    return getPrecio() * 0.30;
}

// Digital.cpp
double Digital::AplicarDescuento() {
    return getPrecio() * 0.12;
}
```

### ¿Por qué cumple el principio?

- `Fisico` y `Digital` pueden usarse donde se espera un `Producto` y `ConvertirPrecio()` sigue funcionando correctamente.
- Ninguna hija cambia lo que el método significa: siempre devuelve **el monto del descuento** y siempre se resta del precio.
- Si mañana se agrega otra clase hija con otro porcentaje, el código que usa `Producto` **no necesita cambiar**.

## Estructura del proyecto

```
Producto.h / Producto.cpp   -> clase base con ConvertirPrecio() y AplicarDescuento() virtual
Fisico.h   / Fisico.cpp     -> descuento del 30 %
Digital.h  / Digital.cpp    -> descuento del 12 %
main.cpp                    -> programa de ejemplo
```

## Salida del programa

Sustitucion de Liskov

[Producto Fisico] 30% Descuento $500. Precio Final: $350

[Producto Digital ] 12% Descuento $120. Precio Final: $105.6

## Cómo ejecutarlo

g++ *.cpp -o programa
./programa        # en Windows: programa.exe

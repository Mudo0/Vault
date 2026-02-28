---
status: borrador
tags:
  - angular
  - frontend
  - componentes
  - eventos
  - comunicacion
created: 2026-01-29
---
# 📡 EventEmitter en [[Angular]]

El `EventEmitter` es un mecanismo fundamental en **[[Angular]]** que permite la emisión de eventos personalizados, facilitando la comunicación entre componentes.

---

## 1. ¿Qué es un EventEmitter?

En términos técnicos, es una clase que extiende de **[[RxJS]]** *Subject*, lo que le permite enviar valores a cualquier observador que esté "suscrito" o escuchando dicho evento.

### Analogía Conceptual
Se puede ilustrar mediante la siguiente analogía:
> Un componente hijo se encuentra en una habitación cerrada y el componente padre espera fuera. El `EventEmitter` funciona como un **intercomunicador** que el hijo posee. Cuando el hijo necesita notificar algo ("Tarea finalizada", "Error detectado"), presiona el botón y el padre, que se encuentra a la escucha, reacciona ante la señal.

---

## 2. 🎯 ¿Para qué sirve?

Su función principal (y el caso de uso predominante) es establecer la **Comunicación de Hijo a Padre**.

* **`@Input`:** Se utiliza para transferir datos hacia abajo (del Padre al Hijo).
* **`@Output` (con `EventEmitter`):** Se utiliza para transferir datos hacia arriba (del Hijo al Padre).

Se implementa cuando ocurre una acción en el componente hijo (ej. clic en un botón, escritura en un *input*, selección de opciones) y se requiere que el componente padre reciba y procese dicha información.

---

## 3. 🛠️ Implementación Paso a Paso

A continuación se presenta un ejemplo de un componente hijo (un botón) que notifica al padre cuántas veces ha sido presionado.

### Paso A: En el Componente Hijo (`hijo.component.ts`)
Se requieren tres elementos clave: el decorador `@Output`, la clase `EventEmitter` y un método que invoque a `.emit()`.

```typescript
import { Component, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-hijo',
  template: `
    <button (click)="notificarAlPadre()">¡Púlsame!</button>
  `
})
export class HijoComponent {
  // 1. Se crea el evento de salida. 
  // <string> indica el tipo de dato a enviar (puede ser number, boolean, object, etc).
  @Output() eventoSaludar = new EventEmitter<string>();

  notificarAlPadre() {
    const mensaje = '¡Hola papá, me hicieron click!';
    
    // 2. Se emite el evento con el valor deseado.
    this.eventoSaludar.emit(mensaje);
  }
}
```

### Paso B: En el Componente Padre (`padre.component.html`)

El padre debe "escuchar" el evento. Para ello se utilizan paréntesis `()` con el nombre exacto de la variable creada en el hijo (`eventoSaludar`).

```html
<app-hijo (eventoSaludar)="recibirMensaje($event)"></app-hijo>

<p>Mensaje recibido: {{ mensajeRecibido }}</p>
```

### Paso C: Lógica del Padre (`padre.component.ts`)

Finalmente, el padre procesa el dato recibido.

```ts
export class PadreComponent {
  mensajeRecibido: string = '';

  recibirMensaje(mensaje: string) {
    console.log('El hijo dijo:', mensaje);
    this.mensajeRecibido = mensaje;
  }
}
```

---

## 🔑 Puntos Clave

1. **`@Output()`:** Es obligatorio colocar este decorador antes de la variable `EventEmitter` para que **[[Angular]]** reconozca la puerta de salida hacia el padre.
    
2. **`.emit(valor)`:** Es la función que "dispara" el evento. El valor es opcional; es posible emitir un evento sin datos simplemente para notificar que una acción ocurrió.
    
3. **`$event`:** En el **[[HTML]]** del padre, `$event` es una palabra reservada. Representa "el dato que proviene desde el emit". Si se omite, el método del padre se ejecutará pero no recibirá el argumento.
# CURSO: APRENDE BLAZOR

# LECCIÓN 37: Interoperatibilidad con JavaScript (InvokeAsync)

1. Abrir la aplicación con Visual Studio 2022 o VSCode

2. Creamos el archivo (example.js) donde definimos nuestra función de JavaScript a invocar desde C#. Localizamos el archivo dentro de una carpeta localizada en wwwroot

```javascript
function generateRandomNumber() {
    return Math.floor(Math.random() * 100); // Returns a random number between 0 and 99
    }
```

3. Creamos el nuevo componente para invocar desde C# la función generateRandomNumber() de JavaScript

```razor
@page "/random"
@inject IJSRuntime JSRuntime

<h3>Random Number Generator</h3>

<p>Generated Random Number: @randomNumber</p>

<button @onclick="GetRandomNumber">Generate Random Number</button>

@code {
    private int randomNumber;

    private async Task GetRandomNumber()
    {
        // Call the JavaScript function 'generateRandomNumber' and get the result
        randomNumber = await JSRuntime.InvokeAsync<int>("generateRandomNumber");
    }
}
```

4. Incluimos en el componente App.razor la localización de nuestro archivo example.js

```razor
<body>
    <Routes @rendermode="InteractiveServer" />
    <script src="_framework/blazor.web.js"></script>
    <script src="js/example.js"></script>
</body>
```

5. Creamos un nuevo NavLink en el componente NavMenu.razor para navegar hacia nuestro nuevo componente

```razor
 <div class="nav-item px-3">
     <NavLink class="nav-link" href="NuevoComponente">
         <span class="bi bi-list-nested-nav-menu" aria-hidden="true"></span> Nuevo Componente
     </NavLink>
 </div>
```

6. Ejecutamos la aplicación



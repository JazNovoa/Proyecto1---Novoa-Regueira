<script>
    import * as d3 from "d3";

    let images2 = [
        "./images/perrogrande1.svg", 
        "./images/perrogrande9.svg", 
        "./images/perrogrande7.svg", 
        "./images/perrogrande10.svg", 
        "./images/perrogrande2.svg", 
        "./images/perrogrande3.svg", 
        "./images/perrogrande4.svg", 
        "./images/perrogrande5.svg", 
        "./images/perrogrande8.svg", 
        "./images/perrogrande6.svg",
    ];

    let images1 = [
        "./images/perrochico1.svg", 
        "./images/perrochico8.svg", 
        "./images/perrochico2.svg", 
        "./images/perrochico3.svg", 
        "./images/perrochico10.svg", 
        "./images/perrochico4.svg", 
        "./images/perrochico7.svg", 
        "./images/perrochico5.svg", 
        "./images/perrochico6.svg", 
        "./images/perrochico9.svg",
    ];

    let serie_a = [21, 33, 42, 54, 63, 71, 77, 84, 92, 98];
    let serie_b = [23, 35, 45, 56, 50, 43, 38, 32, 28, 25];
    let años = [2014, 2015, 2016, 2017, 2018, 2019, 2020, 2021, 2022, 2023];
    
    let altura_a = d3
        .scaleLinear()
        .domain([0, d3.max(serie_a)])
        .range([0, 300]);

    let altura_b = d3
        .scaleLinear()
        .domain([0, d3.max(serie_a)])
        .range([0, 300]);  

    function getImage(index) {
        return images1[index];
    }

    function preload(index) {
        return images2[index];
    }

 
    // Script para desplazar horizontalmente con la rueda del ratón, usando requestAnimationFrame
    function handleWheel(event) {
        if (event.deltaY !== 0) {
            event.preventDefault();
            scrollAmount += event.deltaY * 8;  // Aumentamos la velocidad de scroll multiplicando por 5
            requestAnimationFrame(() => {
                document.querySelector('.scrollable-content').scrollLeft += scrollAmount;
            });
        }
    }

    // Esperar hasta que el DOM esté cargado para añadir el evento
    document.addEventListener('DOMContentLoaded', () => {
        document.addEventListener('wheel', handleWheel);
    });
</script>

<!-- Añadimos el nuevo título -->
<div class="scrollable-content">
    <div class="title-container">
        <img src="./images/titulo.svg" alt="titulo" class="title-image">
    </div>
    <div class="bajada">
        <p>En los <strong>ultimos años</strong>, la cantidad de <strong>perros</strong> en <br>Argentina <strong>ha aumentado</strong>, reflejando una creciente <br>tendencia a tener mascotas.</p>
        <p>A continuación, se presentará un <strong>gráfico</strong> que <br>muestra cómo se ha distribuido esta población <br>canina en términos de tamaño a lo largo de los <br>años, diferenciando cuántos de estos perros son <br><strong>pequeños</strong> y cuántos son <strong>gigantes</strong>.</p>
    </div>
    
    <div class="dos-perros">
        <img src="./images/dosperros-43.png" alt="dos perros">
    </div>

    <!-- Contenedor principal -->
    <div class="container">
        <!-- Codigo para las imágenes -->
        <div class="chart">
            {#each serie_a as num_1, i}
                <div class="item_wrapper">
                    <div class="column">
                        <div class="image-group">
                            <div class="image-left">
                                <p class="label-b">{serie_b[i]}</p> <!-- Texto de serie_b -->
                                <img src={preload(i)} alt="imagen2" style="height: {altura_b(serie_b[i])}px;">
                            </div>
                            <div class="image-right">
                                <p class="label-a">{num_1}</p> <!-- Texto de serie_a -->
                                <img src={getImage(i)} alt="imagen1" style="height: {altura_a(num_1)}px;">
                            </div>
                        </div>
                    </div>
                    <div class="year">{años[i]}</div>
                </div>
            {/each}
        </div>
    </div>

    <div class="chart-wrapper">
        <div class="flourish-embed"><iframe src='https://flo.uri.sh/story/2604732/embed' title='Interactive or visual content' class='flourish-embed-iframe' frameborder='0' scrolling='no' style='width:100%;height:600px;' sandbox='allow-same-origin allow-forms allow-scripts allow-downloads allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation'></iframe><div style='width:100%!;margin-top:4px!important;text-align:right!important;'><a class='flourish-credit' href='https://public.flourish.studio/story/2604732/?utm_source=embed&utm_campaign=story/2604732' target='_top' style='text-decoration:none!important'><img alt='Made with Flourish' src='https://public.flourish.studio/resources/made_with_flourish.svg' style='width:105px!important;height:16px!important;border:none!important;margin:0!important;'> </a></div></div>
        </div>
    
    <div class="chart-wrapper2">
        <div class="flourish-embed"><iframe src='https://flo.uri.sh/visualisation/19394019/embed' title='Interactive or visual content' class='flourish-embed-iframe' frameborder='0' scrolling='no' style='width:100%;height:600px;' sandbox='allow-same-origin allow-forms allow-scripts allow-downloads allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation'></iframe><div style='width:100%!;margin-top:4px!important;text-align:right!important;'><a class='flourish-credit' href='https://public.flourish.studio/visualisation/19394019/?utm_source=embed&utm_campaign=visualisation/19394019' target='_top' style='text-decoration:none!important'><img alt='Made with Flourish' src='https://public.flourish.studio/resources/made_with_flourish.svg' style='width:105px!important;height:16px!important;border:none!important;margin:0!important;'> </a></div></div>
    </div>

    <div class="final">
        <p>Parcial para la materia de “Visualización <br>de Datos” Sección <strong>Araujo</strong></p>
        <p>2024, <strong>UTDT</strong></p>
        <p>Jazmin Novoa y Julieta Regueira</p>
    </div>
</div>



<style>
    /* Estilos para el título */
    .scrollable-content {
    display: flex;
    flex-direction: row;
    justify-content: flex-start; /* Para que el contenido siga desplazándose desde el inicio */
    align-items: center; /* Centra el contenido verticalmente */
    overflow-x: auto; /* Habilita el desplazamiento horizontal */
    height: 100vh; /* Ocupa toda la altura de la pantalla */
    background-color: #000000; /* Color de fondo */
    transform: translateY(-50px); /* Mueve todo el contenido 50px hacia arriba */
    padding-left: 50px; /* Mantiene un pequeño espacio a la izquierda */
}


.title-container {
    flex: 0 0 100vw; /* Ocupa el ancho completo de la pantalla */
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #000000;
}



.bajada{
    flex: 0 0 100vw; /* Ocupa el ancho completo de la pantalla */
    display: flex;
    flex-direction: column;
    justify-content: center;
    font-size: 20px;
    color: white;
    text-align: center;
}

.title-image {
    width: 900px; /* Ajusta el ancho según sea necesario */
    height: auto; /* Mantiene la proporción de la imagen */
    display: block; /* Asegura que la imagen no tenga espacio extra */
}

.dos-perros{
    flex: 0 0 100vw; /* Ocupa el ancho completo de la pantalla */
    display: flex;
    justify-content: center;
    width: 359px;
    height: 188px;
}



    /* El contenido desplazable */
    .container {
    display: flex;
    flex-direction: row;
    gap: 50px;
    align-items: flex-end; /* Asegura que todo el contenido se alinee al final (parte inferior) */
    padding-left: 50px;
}

.chart {
    display: flex;
    justify-content: space-between;
    align-items: flex-end; /* Alinea todo el contenido desde la parte inferior */
    gap: 50px;
}

.item_wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: flex-end; /* Asegura que todo el contenido se mantenga alineado al fondo */
    min-width: 200px;
}

    .column {
        display: flex;
        justify-content: center;
        align-items: end;
        position: relative;
    }

    .image-group {
    display: flex;
    justify-content: space-between;
    align-items: flex-end; /* Asegura que las imágenes estén alineadas desde la parte inferior */
    gap: 10px;
    height: 300px; /* Fija la altura máxima del grupo de imágenes */
    position: relative; /* Esto permitirá que los números se ubiquen encima de las imágenes correctamente */
}

.image-left, .image-right {
    display: flex;
    align-items: flex-end; /* Alinea las imágenes al fondo */
    position: relative;
}

.label-a, .label-b {
    position: absolute;
    top: -20px;
    left: 50%;
    transform: translateX(-50%);
    font-weight: bold;
    font-size: 14px;
}

.label-a {
    color: #f190b8; /* Amarillo para serie_a */
}

.label-b {
    color: #a6cff0; /* Naranja para serie_b */
}

    .year {
        margin-top: 10px;
        color: white;
        text-align: center;
    }

.chart-wrapper{
    flex: 0 0 80vw; 
    display: flex;
    justify-content: center;
    align-content: center;
}

.chart-wrapper2{
    flex: 0 0 40vw; 
    display: flex;
    justify-content: center;
    align-content: center;
    margin-right: 100px;
}


.flourish-embed{
    display: block;
    width: 600px;
    height: auto;
    margin-top: 50px;

}

.final{
    flex: 0 0 100vw; /* Ocupa el ancho completo de la pantalla */
    display: flex;
    flex-direction: column;
    justify-content: center;
    font-size: 20px;
    color: white;
    text-align: center;
}
</style>

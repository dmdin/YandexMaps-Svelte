<svelte:head>
    <title>Map example</title>
    <script src='https://api-maps.yandex.ru/2.1/?lang=ru_RU&amp;apikey=cf1b8beb-bb0c-4563-9d28-c603002dd2ad'
            type="text/javascript" on:load={() => ymaps.ready(loadMap)}>
    </script>
</svelte:head>

<script>
    export let locations = [{
        latitude: 55.75361503443606,
        longitude: 37.620883000000006,
        name: 'Test point'
    }];
    export let center = [55.75361503443606, 37.620883000000006];
    export let zoom = 17;

    let Loaded = false;

    function loadMap() {
        var myMap = new ymaps.Map("map", {
            center: center,
            zoom: zoom
        });
        // Создаем геообъект с типом геометрии "Точка".
        const points = myMap.geoObjects;
        locations.forEach(location => {
            points.add(new ymaps.Placemark(
                [location.latitude, location.longitude],
                    {balloonContent: location.name},
                    {
            }));
        });
        Loaded = true;
    }
</script>

<div>
    {#if Loaded === false}
        <h1>Loading...</h1>
    {/if}
</div>
<div id="map"></div>

<style>
    #map {
        width: 720px;
        height: 540px;
    }
</style>
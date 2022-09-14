<script>

    import {onMount} from 'svelte';
    import { check_outros } from 'svelte/internal';
    import "../app.css";

    let shownType;

    let charactername;
    let characterheight;
    let charactermass;
    let characterhair_color;
    let characterskin_color;
    let charactereye_color;
    let characterbirth_year;
    let charactergender;
    let characterhomeworld;
    let characterfilms = "";
    let characterspecies = "";
    let charactervehicles = "";
    let characterstarships = "";



    function GetPerson()
    {
        shownType = "Person";

        fetch('https://swapi.dev/api/people/'+ getRandomInt(80))
		.then((response) => response.json())
		.then((fetchedPerson) => {
            charactername = fetchedPerson.name;
            characterheight = fetchedPerson.height;
            charactermass = fetchedPerson.mass;
            characterhair_color = fetchedPerson.hair_color;
            characterskin_color = fetchedPerson.skin_color;
            charactereye_color = fetchedPerson.eye_color;
            characterbirth_year = fetchedPerson.birth_year;
            charactergender = fetchedPerson.gender;
            characterhomeworld = fetchedPerson.homeworld;
            characterfilms = fetchedPerson.films;
            characterspecies = fetchedPerson.species;
            charactervehicles = fetchedPerson.vehicles;
            characterstarships = fetchedPerson.starships;
		}) 
       

        characterfilms = characterfilms.toString().split(',',100);
        characterspecies = characterspecies.toString().split(',',100);
        charactervehicles = charactervehicles.toString().split(',',100);
        characterstarships = characterstarships.toString().split(',',100);
    }

    function GetSpecificPerson(url)
    {
        shownType = "Person";

        fetch(url)
		.then((response) => response.json())
		.then((fetchedPerson) => {
            charactername = fetchedPerson.name;
            characterheight = fetchedPerson.height;
            charactermass = fetchedPerson.mass;
            characterhair_color = fetchedPerson.hair_color;
            characterskin_color = fetchedPerson.skin_color;
            charactereye_color = fetchedPerson.eye_color;
            characterbirth_year = fetchedPerson.birth_year;
            charactergender = fetchedPerson.gender;
            characterhomeworld = fetchedPerson.homeworld;
            characterfilms = fetchedPerson.films;
            characterspecies = fetchedPerson.species;
            charactervehicles = fetchedPerson.vehicles;
            characterstarships = fetchedPerson.starships;
		}) 
       

        characterfilms = characterfilms.toString().split(',',100);
        characterspecies = characterspecies.toString().split(',',100);
        charactervehicles = charactervehicles.toString().split(',',100);
        characterstarships = characterstarships.toString().split(',',100);
    }



    let filmTitle;
    let filmEpisode;
    let filmDirector;
    let filmProducer;
    let filmReleaseDate;
    let filmCharacters = "";
    let filmPlanets = "";
    let filmStarships ="";
    let filmVehicels = "";
    let filmSpecies = "";


    function GetSpecificFilm(url)
    {
        shownType = "Film";

        fetch(url)
		.then((response) => response.json())
		.then((fetchedFilm) => {
            filmTitle = fetchedFilm.title;
            filmEpisode = fetchedFilm.episode_id;
            filmDirector = fetchedFilm.director;
            filmProducer = fetchedFilm.producer;
            filmReleaseDate = fetchedFilm.release_date;
            filmCharacters = fetchedFilm.characters;
            filmPlanets = fetchedFilm.planets;
            filmStarships = fetchedFilm.starships;
            filmVehicels = fetchedFilm.vehicles;
            filmSpecies = fetchedFilm.species;
		}) 

        filmSpecies = filmSpecies.toString().split(',',100);
        filmVehicels = filmVehicels.toString().split(',',100);
        filmStarships = filmStarships.toString().split(',',100);
        filmPlanets = filmPlanets.toString().split(',',100);
        
    }


    let planetName;
    let planetRotationPeriod;
    let planetorbitalPeriod;
    let planetDiameter;
    let planetClimate;
    let planetGravity;
    let planetTerrain;
    let planetSurfaceWater;
    let planetPopulation;
    let planetResidents = "";
    let planetFilm = "";

    function GetSpecificPlanet(url)
    {
        shownType = "Planet";

        fetch(url)
        .then((response) => response.json())
        .then((fetchedPlanet) => {
            planetName = fetchedPlanet.name;
            planetRotationPeriod = fetchedPlanet.rotation_period;
            planetorbitalPeriod = fetchedPlanet.orbital_period;
            planetDiameter = fetchedPlanet.diameter;
            planetClimate = fetchedPlanet.climate;
            planetGravity = fetchedPlanet.gravity;
            planetTerrain = fetchedPlanet.terrain;
            planetSurfaceWater = fetchedPlanet.surface_water;
            planetPopulation = fetchedPlanet.population;
            planetResidents = fetchedPlanet.residents;
            planetFilm = fetchedPlanet.films;
            
        }) 

        planetResidents = planetResidents.toString().split(',',100);
        planetFilm = planetFilm.toString().split(',',100);
    }

    function getRandomInt(max){
        return Math.floor(Math.random() * max);
    }
</script>

<div class="flex items-center justify-center pt-6 pb-6">
    <button on:click="{GetPerson}" class="w-96 h-10 px-10 text-indigo-100 transition-colors duration-150 bg-indigo-700 rounded-lg focus:shadow-outline hover:bg-indigo-800" >Load Person</button>
</div>

<main>
    <body>
        

        {#if shownType === undefined}
        <h5 class="font-bold">Press the button</h5>
        {:else if shownType === "Person"}
        <h5 class="font-bold">{charactername}</h5>
        <p><strong>Height</strong>: {characterheight}</p>
        <p><strong>Mass</strong>: {charactermass}</p>
        <p><strong>Hair Color</strong>: {characterhair_color}</p>
        <p><strong>Skin Color</strong>: {characterskin_color}</p>
        <p><strong>Eye Color</strong>: {charactereye_color}</p>
        <p><strong>Birth Year</strong>: {characterbirth_year}</p>
        <p><strong>Gender</strong>: {charactergender}</p>
        <span onmouseover="this.style.cursor='pointer'" onmouseout="this.style.cursor='default'" on:click="{GetSpecificPlanet(characterhomeworld)}">
            <p><strong>Home World</strong>: {characterhomeworld}</p>
        </span>
        <p><strong>Films</strong>:</p>
        <ul>
            {#each characterfilms as film}
            <span onmouseover="this.style.cursor='pointer'" onmouseout="this.style.cursor='default'" on:click="{GetSpecificFilm(film)}">
                <li>{film}</li>
            </span>
            {/each}
        </ul>
        <p><strong>Speices</strong>:</p>
        <ul>
            {#each characterspecies as specie}
            <li>{specie}</li>
            {/each}
        </ul>
        <p><strong>Vehicles</strong>:</p>
        <ul>
            {#each charactervehicles as vehicle}
            <li>{vehicle}</li>
            {/each}
        </ul>
            <p><strong>Starships</strong>:</p>
        <ul>
            {#each characterstarships as starship}
                <li>{starship}</li>
            {/each}
        </ul>

        {:else if shownType === "Film"}

        <h5 class="font-bold">{filmTitle}</h5>
        <p><strong>Episode</strong>: {filmEpisode}</p>
        <p><strong>Director</strong>: {filmDirector}</p>
        <p><strong>Producer</strong>: {filmProducer}</p>
        <p><strong>Release Date</strong>: {filmReleaseDate}</p>
        <p><strong>Characters</strong>:</p>
        <ul>
            {#each filmCharacters as character}
            <span onmouseover="this.style.cursor='pointer'" onmouseout="this.style.cursor='default'" on:click="{GetSpecificPerson(character)}">
                <li>{character}</li>
            </span>
            {/each}
        </ul>
        <p><strong>Speices</strong>:</p>
        <ul>
            {#each filmSpecies as specie}
            <li>{specie}</li>
            {/each}
        </ul>
        <p><strong>Vehicles</strong>:</p>
        <ul>
            {#each filmVehicels as vehicle}
            <li>{vehicle}</li>
            {/each}
        </ul>
            <p><strong>Starships</strong>:</p>
        <ul>
            {#each filmStarships as starship}
                <li>{starship}</li>
            {/each}
        </ul>
        <p><strong>Planets</strong>: </p>
        <ul>
            {#each filmPlanets as planet}
            <span onmouseover="this.style.cursor='pointer'" onmouseout="this.style.cursor='default'" on:click="{GetSpecificPlanet(planet)}">
                <li>{planet}</li>
            </span>
            {/each}
        </ul>

        {:else if shownType === "Planet"}

        <h5 class="font-bold">{planetName}</h5>
        <p><strong>Rotation Period</strong>: {planetRotationPeriod}</p>
        <p><strong>Orbital Period</strong>: {planetorbitalPeriod}</p>
        <p><strong>Diameter</strong>: {planetDiameter}</p>
        <p><strong>Climate</strong>: {planetClimate}</p>
        <p><strong>Gravity</strong>: {planetGravity}</p>
        <p><strong>Terrain</strong>: {planetTerrain}</p>
        <p><strong>Surface Water</strong>: {planetSurfaceWater}</p>
        <p><strong>Population</strong>: {planetPopulation}</p>
        <p><strong>Residents</strong>:</p>
        <ul>
            {#each planetResidents as character}
            <span onmouseover="this.style.cursor='pointer'" onmouseout="this.style.cursor='default'" on:click="{GetSpecificPerson(character)}">
                <li>{character}</li>
            </span>
            {/each}
        </ul>
        <p><strong>Films</strong>:</p>
        <ul>
            {#each planetFilm as film}
            <span onmouseover="this.style.cursor='pointer'" onmouseout="this.style.cursor='default'" on:click="{GetSpecificFilm(film)}">
                <li>{film}</li>
            </span>
            {/each}
        </ul>


        {/if}


        
            
            
        </body>
    
</main>
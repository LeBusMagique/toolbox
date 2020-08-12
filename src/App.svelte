<svelte:options tag="lbm-toolbox" accessors={false} />

<script>

	import { onMount } from 'svelte';

	let show = false;
	let lastRssTitle = false;
	let lastRssUrl = false;

	function toggleToolbar() {
		show = !show;
	}

	onMount(() => {
		loadXMLDoc();
	});

	function loadXMLDoc() {
	  var xmlhttp = new XMLHttpRequest();
	  xmlhttp.onreadystatechange = function() {
	    if (this.readyState == 4 && this.status == 200) {
	      readXMLDoc(this);
	    }
	  };
	  xmlhttp.open("GET", "https://www.lebusmagique.fr/blog/do/rss.xml", true);
	  xmlhttp.send();
	}

	function readXMLDoc(xml) {
	  var x, y, xmlDoc, title, url;
	  xmlDoc = xml.responseXML;
	  x = xmlDoc.getElementsByTagName("title");
	  y = xmlDoc.getElementsByTagName("link");
		title = x[1].childNodes[0].nodeValue;
		url = y[1].childNodes[0].nodeValue;
		lastRssTitle = (typeof(title) !== 'undefined') ? title : false;
		lastRssUrl = (typeof(url) !== 'undefined') ? url : false;

	}
</script>

<style>
	* {
		font-family: Arial, Helvetica, sans-serif;
	}
	#button {
		position: fixed;
		top: calc(50% - 1.5em - 1px);
		left: 0;
		z-index: 10001;
		width: 3em;
		height: 3em;
		display: flex;
		border-radius: 0 4px 4px 0;
		background: #fff;
		padding: 0;
		cursor: pointer;
		align-items: center;
		justify-content: center;
		background: #f44336;
		color: #fff;
		fill: #fff;
		box-shadow: 0 0 10px rgba(0, 0, 0, .5);
		border: 2px solid #fff;
    border-left: 0;
	}

	#button svg {
		width: 1em;
		color: #fff;
	}

	#button svg.big {
		width: 1.5em;
	}

	#overlay {
		background: rgba(0, 0, 0, .75);
		position: fixed;
		width: 100%;
		height: 100%;
		top: 0;
		bottom: 0;
		left: 0;
		right: 0;
		z-index: 10000;
		overflow-y: auto;
	}

	#wrap {
		display: flex;
		align-items: center;
		justify-content: center;
		height: 100%;
		min-height: 700px;
	}

	#tools {
		display: grid;
	  height: 80%;
	  grid-template-rows: repeat(7, 1fr);
	  grid-template-columns: repeat(2, 1fr);
	  grid-gap: 1em;
		max-width: 60em;
		width: 100%;
		padding: 0;
		margin: 0 4em;
	}

	#tools li {
		display: flex;
	  justify-content: center;
	  align-items: center;
		grid-row: span 1;
    grid-column: span 1;
	}

	#tools li.high {
		grid-row: span 2;
    grid-column: span 1;
	}

	#tools li.large {
		grid-row: span 1;
    grid-column: span 2;
	}

	#tools li a {
		text-decoration: none;
		color: #fff;
		font-weight: bold;
		display: flex;
		width: 100%;
		height: 100%;
		align-content: center;
		align-items: center;
		justify-content: center;
		flex-wrap: wrap;
		background: #f44336;
		border-radius: 4px;
		box-shadow: 0 0 10px rgba(0, 0, 0, .5);
		border: 2px solid #fff;
		padding: .75em 1em;
		box-sizing: border-box;
	}

	#tools li a span {
		display: block;
		width: 100%;
		text-align: center;
	}

	#tools li a span svg{
		display: block;
    width: 1.5em;
		text-align: center;
	}

	#tools li a .subtitle {
		font-weight: normal;
		font-size: .8em;
	}

	@media screen and (max-width: 600px) {
		#tools {
		  grid-template-columns: repeat(1, 1fr);
			grid-template-rows: repeat(10, 1fr);
		}

		#tools li.high {
			grid-row: span 1;
	    grid-column: span 1;
		}

		#tools li.large {
			grid-row: span 1;
	    grid-column: span 1;
		}
	}

	#tools li.rss a {
		background: none;
		border: 0;
		box-shadow: none;
	}
</style>

<a on:click="{toggleToolbar}" id="button" href="#!">
	{#if show}
		<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 352 512"><path d="M242.72 256l100.07-100.07c12.28-12.28 12.28-32.19 0-44.48l-22.24-22.24c-12.28-12.28-32.19-12.28-44.48 0L176 189.28 75.93 89.21c-12.28-12.28-32.19-12.28-44.48 0L9.21 111.45c-12.28 12.28-12.28 32.19 0 44.48L109.28 256 9.21 356.07c-12.28 12.28-12.28 32.19 0 44.48l22.24 22.24c12.28 12.28 32.2 12.28 44.48 0L176 322.72l100.07 100.07c12.28 12.28 32.2 12.28 44.48 0l22.24-22.24c12.28-12.28 12.28-32.19 0-44.48L242.72 256z"/></svg>
	{:else}
		<svg class="big" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path d="M502.63 214.63l-45.25-45.25c-6-6-14.14-9.37-22.63-9.37H384V80c0-26.51-21.49-48-48-48H176c-26.51 0-48 21.49-48 48v80H77.25c-8.49 0-16.62 3.37-22.63 9.37L9.37 214.63c-6 6-9.37 14.14-9.37 22.63V320h128v-16c0-8.84 7.16-16 16-16h32c8.84 0 16 7.16 16 16v16h128v-16c0-8.84 7.16-16 16-16h32c8.84 0 16 7.16 16 16v16h128v-82.75c0-8.48-3.37-16.62-9.37-22.62zM320 160H192V96h128v64zm64 208c0 8.84-7.16 16-16 16h-32c-8.84 0-16-7.16-16-16v-16H192v16c0 8.84-7.16 16-16 16h-32c-8.84 0-16-7.16-16-16v-16H0v96c0 17.67 14.33 32 32 32h448c17.67 0 32-14.33 32-32v-96H384v16z"/></svg>
	{/if}
</a>

{#if show}
	<div id="overlay">
		<div id="wrap">
			<ul id="tools">
				<li class="large">
					<a href="https://www.lebusmagique.fr" target="_self">
						<span class="title">Le Bus Magique</span>
						<span class="subtitle">&laquo; Retourner au site principal</span>
					</a>
				</li>
				<li>
					<a href="https://www.lebusmagique.fr/pages/outils-gw2/succes-quotidiens.html" target="_blank">
						<span class="title">Succès quotidiens</span>
					</a>
				</li>
				<li class="high">
					<a href="https://event.lebusmagique.fr/" target="_blank">
						<span class="title">Événements du Bus Magique</span>
						<span class="subtitle">Activités et sorties de nos conducteurs et organisateurs</span>
					</a>
				</li>
				<li>
					<a href="https://www.lebusmagique.fr/pages/outils-gw2/les-world-boss.html" target="_blank">
						<span class="title">Timer des world boss</span>
						<span class="subtitle">Tyrie Centrale</span>
					</a>
				</li>
				<li class="high">
					<a href="https://www.lebusmagique.fr/pages/outils-gw2/timer-wb-et-hot.html" target="_blank">
						<span class="title">Timer des métas & world boss</span>
						<span class="subtitle">Heart of Thorns, Path of Fire et Monde vivant</span>
					</a>
				</li>
				<li>
					<a href="https://outils.lebusmagique.fr/twitch" target="_blank">
						<span class="title">Guild&nbsp;Wars&nbsp;2 sur Twitch</span>
						<span class="subtitle">Nos streamers préférés et partenaires</span>
					</a>
				</li>
				<li>
					<a href="https://discord.gg/WRFnwph" target="_blank">
						<span class="title">Serveur Discord du Bus Magique</span>
					</a>
				</li>
				<li>
					<a href="https://outils.lebusmagique.fr/carte-interactive/" target="_blank">
						<span class="title"> 		<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 352 512"><path d="M560.02 32c-1.96 0-3.98.37-5.96 1.16L384.01 96H384L212 35.28A64.252 64.252 0 0 0 191.76 32c-6.69 0-13.37 1.05-19.81 3.14L20.12 87.95A32.006 32.006 0 0 0 0 117.66v346.32C0 473.17 7.53 480 15.99 480c1.96 0 3.97-.37 5.96-1.16L192 416l172 60.71a63.98 63.98 0 0 0 40.05.15l151.83-52.81A31.996 31.996 0 0 0 576 394.34V48.02c0-9.19-7.53-16.02-15.98-16.02zM224 90.42l128 45.19v285.97l-128-45.19V90.42zM48 418.05V129.07l128-44.53v286.2l-.64.23L48 418.05zm480-35.13l-128 44.53V141.26l.64-.24L528 93.95v288.97z"/></svg>
						Carte interactive
					  </span>
					</a>
				</li>
				<li class="high">
					<a href="https://www.lebusmagique.fr/pages/infos/comment-nous-rejoindre.html" target="_blank">
						<span class="title">Rejoignez la communauté</span>
						<span class="subtitle">Envie de monter à bord du Bus&nbsp;?</span>
					</a>
				</li>
				<li>
					<a href="https://www.lebusmagique.fr/pages/outils-gw2/banque-de-materiaux-et-portefeuille.html" target="_blank">
						<span class="title">Banque de matériaux & portefeuille</span>
					</a>
				</li>
				<li>
					<a href="https://www.lebusmagique.fr/pages/guides/home/l-instance-personnelle.html" target="_blank">
						<span class="title">Instance personnelle</span>
						<span class="subtitle">Améliorez votre zone personnelle</span>
					</a>
				</li>
				<li>
					<a href="https://outils.lebusmagique.fr/observatory/" target="_blank">
						<span class="title">GW2 Observatory</span>
						<span class="subtitle">Remontez la chronologie de vos personnages</span>
					</a>
				</li>
				<li class="large">
					<a href="https://www.lebusmagique.fr/pages/outils-gw2/decorations-de-hall-de-guilde.html" target="_blank">
						<span class="title">Décorations de hall de guilde</span>
						<span class="subtitle">Aperçus, recettes et listes d'ingrédients</span>
					</a>
				</li>
				{#if lastRssTitle && lastRssUrl}
					<li class="large rss">
						<a href="{lastRssUrl}" target="_blank">
							<span class="title">{lastRssTitle}</span>
							<span class="subtitle">&uarr; Dernier article publié sur notre site &uarr;</span>
						</a>
					</li>
				{/if}
			</ul>
		</div>
	</div>
{/if}

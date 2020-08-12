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
		#tools li a:hover {
			border: 4px solid  #6f69bf;
		}

	#tools li a span {
		display: block;
		width: 100%;
		text-align: center;
	}

	#tools li a img{
		display: block;
    width: auto;
		height: 1.5em;
		margin-bottom: 0.5em;
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
					  <img src=" data:image/svg+xml;base64,PHN2ZyBhcmlhLWhpZGRlbj0idHJ1ZSIgZm9jdXNhYmxlPSJmYWxzZSIgZGF0YS1wcmVmaXg9ImZhcyIgZGF0YS1pY29uPSJjYWxlbmRhci1jaGVjayIgY2xhc3M9InN2Zy1pbmxpbmUtLWZhIGZhLWNhbGVuZGFyLWNoZWNrIGZhLXctMTQiIHJvbGU9ImltZyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB2aWV3Qm94PSIwIDAgNDQ4IDUxMiI+PHBhdGggZmlsbD0iI2ZmZmZmZiIgZD0iTTQzNiAxNjBIMTJjLTYuNjI3IDAtMTItNS4zNzMtMTItMTJ2LTM2YzAtMjYuNTEgMjEuNDktNDggNDgtNDhoNDhWMTJjMC02LjYyNyA1LjM3My0xMiAxMi0xMmg0MGM2LjYyNyAwIDEyIDUuMzczIDEyIDEydjUyaDEyOFYxMmMwLTYuNjI3IDUuMzczLTEyIDEyLTEyaDQwYzYuNjI3IDAgMTIgNS4zNzMgMTIgMTJ2NTJoNDhjMjYuNTEgMCA0OCAyMS40OSA0OCA0OHYzNmMwIDYuNjI3LTUuMzczIDEyLTEyIDEyek0xMiAxOTJoNDI0YzYuNjI3IDAgMTIgNS4zNzMgMTIgMTJ2MjYwYzAgMjYuNTEtMjEuNDkgNDgtNDggNDhINDhjLTI2LjUxIDAtNDgtMjEuNDktNDgtNDhWMjA0YzAtNi42MjcgNS4zNzMtMTIgMTItMTJ6bTMzMy4yOTYgOTUuOTQ3bC0yOC4xNjktMjguMzk4Yy00LjY2Ny00LjcwNS0xMi4yNjUtNC43MzYtMTYuOTctLjA2OEwxOTQuMTIgMzY0LjY2NWwtNDUuOTgtNDYuMzUyYy00LjY2Ny00LjcwNS0xMi4yNjYtNC43MzYtMTYuOTcxLS4wNjhsLTI4LjM5NyAyOC4xN2MtNC43MDUgNC42NjctNC43MzYgMTIuMjY1LS4wNjggMTYuOTdsODIuNjAxIDgzLjI2OWM0LjY2NyA0LjcwNSAxMi4yNjUgNC43MzYgMTYuOTcuMDY4bDE0Mi45NTMtMTQxLjgwNWM0LjcwNS00LjY2NyA0LjczNi0xMi4yNjUuMDY4LTE2Ljk3eiI+PC9wYXRoPjwvc3ZnPg0K" />
						<span class="title">Succès quotidiens</span>
					</a>
				</li>
				<li class="high">
					<a href="https://event.lebusmagique.fr/" target="_blank">
					  <img src="data:image/svg+xml;base64,PHN2ZyBhcmlhLWhpZGRlbj0idHJ1ZSIgZm9jdXNhYmxlPSJmYWxzZSIgZGF0YS1wcmVmaXg9ImZhciIgZGF0YS1pY29uPSJjYWxlbmRhci1hbHQiIGNsYXNzPSJzdmctaW5saW5lLS1mYSBmYS1jYWxlbmRhci1hbHQgZmEtdy0xNCIgcm9sZT0iaW1nIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA0NDggNTEyIj48cGF0aCBmaWxsPSIjZmZmZmZmIiBkPSJNMTQ4IDI4OGgtNDBjLTYuNiAwLTEyLTUuNC0xMi0xMnYtNDBjMC02LjYgNS40LTEyIDEyLTEyaDQwYzYuNiAwIDEyIDUuNCAxMiAxMnY0MGMwIDYuNi01LjQgMTItMTIgMTJ6bTEwOC0xMnYtNDBjMC02LjYtNS40LTEyLTEyLTEyaC00MGMtNi42IDAtMTIgNS40LTEyIDEydjQwYzAgNi42IDUuNCAxMiAxMiAxMmg0MGM2LjYgMCAxMi01LjQgMTItMTJ6bTk2IDB2LTQwYzAtNi42LTUuNC0xMi0xMi0xMmgtNDBjLTYuNiAwLTEyIDUuNC0xMiAxMnY0MGMwIDYuNiA1LjQgMTIgMTIgMTJoNDBjNi42IDAgMTItNS40IDEyLTEyem0tOTYgOTZ2LTQwYzAtNi42LTUuNC0xMi0xMi0xMmgtNDBjLTYuNiAwLTEyIDUuNC0xMiAxMnY0MGMwIDYuNiA1LjQgMTIgMTIgMTJoNDBjNi42IDAgMTItNS40IDEyLTEyem0tOTYgMHYtNDBjMC02LjYtNS40LTEyLTEyLTEyaC00MGMtNi42IDAtMTIgNS40LTEyIDEydjQwYzAgNi42IDUuNCAxMiAxMiAxMmg0MGM2LjYgMCAxMi01LjQgMTItMTJ6bTE5MiAwdi00MGMwLTYuNi01LjQtMTItMTItMTJoLTQwYy02LjYgMC0xMiA1LjQtMTIgMTJ2NDBjMCA2LjYgNS40IDEyIDEyIDEyaDQwYzYuNiAwIDEyLTUuNCAxMi0xMnptOTYtMjYwdjM1MmMwIDI2LjUtMjEuNSA0OC00OCA0OEg0OGMtMjYuNSAwLTQ4LTIxLjUtNDgtNDhWMTEyYzAtMjYuNSAyMS41LTQ4IDQ4LTQ4aDQ4VjEyYzAtNi42IDUuNC0xMiAxMi0xMmg0MGM2LjYgMCAxMiA1LjQgMTIgMTJ2NTJoMTI4VjEyYzAtNi42IDUuNC0xMiAxMi0xMmg0MGM2LjYgMCAxMiA1LjQgMTIgMTJ2NTJoNDhjMjYuNSAwIDQ4IDIxLjUgNDggNDh6bS00OCAzNDZWMTYwSDQ4djI5OGMwIDMuMyAyLjcgNiA2IDZoMzQwYzMuMyAwIDYtMi43IDYtNnoiPjwvcGF0aD48L3N2Zz4NCg==" />
						<span class="title">Événements du Bus Magique</span>
						<span class="subtitle">Activités et sorties de nos conducteurs et organisateurs</span>
					</a>
				</li>
				<li>
					<a href="https://www.lebusmagique.fr/pages/outils-gw2/les-world-boss.html" target="_blank">
					  <img src="data:image/svg+xml;base64,PHN2ZyBhcmlhLWhpZGRlbj0idHJ1ZSIgZm9jdXNhYmxlPSJmYWxzZSIgZGF0YS1wcmVmaXg9ImZhcyIgZGF0YS1pY29uPSJob3VyZ2xhc3MtaGFsZiIgY2xhc3M9InN2Zy1pbmxpbmUtLWZhIGZhLWhvdXJnbGFzcy1oYWxmIGZhLXctMTIiIHJvbGU9ImltZyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB2aWV3Qm94PSIwIDAgMzg0IDUxMiI+PHBhdGggZmlsbD0iI2ZmZmZmZiIgZD0iTTM2MCAwSDI0QzEwLjc0NSAwIDAgMTAuNzQ1IDAgMjR2MTZjMCAxMy4yNTUgMTAuNzQ1IDI0IDI0IDI0IDAgOTAuOTY1IDUxLjAxNiAxNjcuNzM0IDEyMC44NDIgMTkyQzc1LjAxNiAyODAuMjY2IDI0IDM1Ny4wMzUgMjQgNDQ4Yy0xMy4yNTUgMC0yNCAxMC43NDUtMjQgMjR2MTZjMCAxMy4yNTUgMTAuNzQ1IDI0IDI0IDI0aDMzNmMxMy4yNTUgMCAyNC0xMC43NDUgMjQtMjR2LTE2YzAtMTMuMjU1LTEwLjc0NS0yNC0yNC0yNCAwLTkwLjk2NS01MS4wMTYtMTY3LjczNC0xMjAuODQyLTE5MkMzMDguOTg0IDIzMS43MzQgMzYwIDE1NC45NjUgMzYwIDY0YzEzLjI1NSAwIDI0LTEwLjc0NSAyNC0yNFYyNGMwLTEzLjI1NS0xMC43NDUtMjQtMjQtMjR6bS03NS4wNzggMzg0SDk5LjA4YzE3LjA1OS00Ni43OTcgNTIuMDk2LTgwIDkyLjkyLTgwIDQwLjgyMSAwIDc1Ljg2MiAzMy4xOTYgOTIuOTIyIDgwem0uMDE5LTI1Nkg5OS4wNzhDOTEuOTg4IDEwOC41NDggODggODYuNzQ4IDg4IDY0aDIwOGMwIDIyLjgwNS0zLjk4NyA0NC41ODctMTEuMDU5IDY0eiI+PC9wYXRoPjwvc3ZnPg0K" />
						<span class="title">Timer des world boss</span>
						<span class="subtitle">Tyrie Centrale</span>
					</a>
				</li>
				<li class="high">
					<a href="https://www.lebusmagique.fr/pages/outils-gw2/timer-wb-et-hot.html" target="_blank">
					  <img src="data:image/svg+xml;base64,PHN2ZyBhcmlhLWhpZGRlbj0idHJ1ZSIgZm9jdXNhYmxlPSJmYWxzZSIgZGF0YS1wcmVmaXg9ImZhciIgZGF0YS1pY29uPSJjbG9jayIgY2xhc3M9InN2Zy1pbmxpbmUtLWZhIGZhLWNsb2NrIGZhLXctMTYiIHJvbGU9ImltZyIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB2aWV3Qm94PSIwIDAgNTEyIDUxMiI+PHBhdGggZmlsbD0iI2ZmZmZmZiIgZD0iTTI1NiA4QzExOSA4IDggMTE5IDggMjU2czExMSAyNDggMjQ4IDI0OCAyNDgtMTExIDI0OC0yNDhTMzkzIDggMjU2IDh6bTAgNDQ4Yy0xMTAuNSAwLTIwMC04OS41LTIwMC0yMDBTMTQ1LjUgNTYgMjU2IDU2czIwMCA4OS41IDIwMCAyMDAtODkuNSAyMDAtMjAwIDIwMHptNjEuOC0xMDQuNGwtODQuOS02MS43Yy0zLjEtMi4zLTQuOS01LjktNC45LTkuN1YxMTZjMC02LjYgNS40LTEyIDEyLTEyaDMyYzYuNiAwIDEyIDUuNCAxMiAxMnYxNDEuN2w2Ni44IDQ4LjZjNS40IDMuOSA2LjUgMTEuNCAyLjYgMTYuOEwzMzQuNiAzNDljLTMuOSA1LjMtMTEuNCA2LjUtMTYuOCAyLjZ6Ij48L3BhdGg+PC9zdmc+DQo=" />
						<span class="title">Timer des métas & world boss</span>
						<span class="subtitle">Heart of Thorns, Path of Fire et Monde vivant</span>
					</a>
				</li>
				<li>
					<a href="https://outils.lebusmagique.fr/twitch" target="_blank">
					  <img src="data:image/svg+xml;base64,PHN2ZyBhcmlhLWhpZGRlbj0idHJ1ZSIgZm9jdXNhYmxlPSJmYWxzZSIgZGF0YS1wcmVmaXg9ImZhYiIgZGF0YS1pY29uPSJ0d2l0Y2giIGNsYXNzPSJzdmctaW5saW5lLS1mYSBmYS10d2l0Y2ggZmEtdy0xNiIgcm9sZT0iaW1nIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA1MTIgNTEyIj48cGF0aCBmaWxsPSIjZmZmZmZmIiBkPSJNMzkxLjE3LDEwMy40N0gzNTIuNTR2MTA5LjdoMzguNjNaTTI4NSwxMDNIMjQ2LjM3VjIxMi43NUgyODVaTTEyMC44MywwLDI0LjMxLDkxLjQyVjQyMC41OEgxNDAuMTRWNTEybDk2LjUzLTkxLjQyaDc3LjI1TDQ4Ny42OSwyNTZWMFpNNDQ5LjA3LDIzNy43NWwtNzcuMjIsNzMuMTJIMjk0LjYxbC02Ny42LDY0di02NEgxNDAuMTRWMzYuNThINDQ5LjA3WiI+PC9wYXRoPjwvc3ZnPg0K" />
						<span class="title">Guild&nbsp;Wars&nbsp;2 sur Twitch</span>
						<span class="subtitle">Nos streamers préférés et partenaires</span>
					</a>
				</li>
				<li>
					<a href="https://discord.gg/WRFnwph" target="_blank">
					<img src="data:image/svg+xml;base64,PHN2ZyBhcmlhLWhpZGRlbj0idHJ1ZSIgZm9jdXNhYmxlPSJmYWxzZSIgZGF0YS1wcmVmaXg9ImZhYiIgZGF0YS1pY29uPSJkaXNjb3JkIiBjbGFzcz0ic3ZnLWlubGluZS0tZmEgZmEtZGlzY29yZCBmYS13LTE0IiByb2xlPSJpbWciIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgdmlld0JveD0iMCAwIDQ0OCA1MTIiPjxwYXRoIGZpbGw9IiNmZmZmZmYiIGQ9Ik0yOTcuMjE2IDI0My4yYzAgMTUuNjE2LTExLjUyIDI4LjQxNi0yNi4xMTIgMjguNDE2LTE0LjMzNiAwLTI2LjExMi0xMi44LTI2LjExMi0yOC40MTZzMTEuNTItMjguNDE2IDI2LjExMi0yOC40MTZjMTQuNTkyIDAgMjYuMTEyIDEyLjggMjYuMTEyIDI4LjQxNnptLTExOS41NTItMjguNDE2Yy0xNC41OTIgMC0yNi4xMTIgMTIuOC0yNi4xMTIgMjguNDE2czExLjc3NiAyOC40MTYgMjYuMTEyIDI4LjQxNmMxNC41OTIgMCAyNi4xMTItMTIuOCAyNi4xMTItMjguNDE2LjI1Ni0xNS42MTYtMTEuNTItMjguNDE2LTI2LjExMi0yOC40MTZ6TTQ0OCA1Mi43MzZWNTEyYy02NC40OTQtNTYuOTk0LTQzLjg2OC0zOC4xMjgtMTE4Ljc4NC0xMDcuNzc2bDEzLjU2OCA0Ny4zNkg1Mi40OEMyMy41NTIgNDUxLjU4NCAwIDQyOC4wMzIgMCAzOTguODQ4VjUyLjczNkMwIDIzLjU1MiAyMy41NTIgMCA1Mi40OCAwaDM0My4wNEM0MjQuNDQ4IDAgNDQ4IDIzLjU1MiA0NDggNTIuNzM2em0tNzIuOTYgMjQyLjY4OGMwLTgyLjQzMi0zNi44NjQtMTQ5LjI0OC0zNi44NjQtMTQ5LjI0OC0zNi44NjQtMjcuNjQ4LTcxLjkzNi0yNi44OC03MS45MzYtMjYuODhsLTMuNTg0IDQuMDk2YzQzLjUyIDEzLjMxMiA2My43NDQgMzIuNTEyIDYzLjc0NCAzMi41MTItNjAuODExLTMzLjMyOS0xMzIuMjQ0LTMzLjMzNS0xOTEuMjMyLTcuNDI0LTkuNDcyIDQuMzUyLTE1LjEwNCA3LjQyNC0xNS4xMDQgNy40MjRzMjEuMjQ4LTIwLjIyNCA2Ny4zMjgtMzMuNTM2bC0yLjU2LTMuMDcycy0zNS4wNzItLjc2OC03MS45MzYgMjYuODhjMCAwLTM2Ljg2NCA2Ni44MTYtMzYuODY0IDE0OS4yNDggMCAwIDIxLjUwNCAzNy4xMiA3OC4wOCAzOC45MTIgMCAwIDkuNDcyLTExLjUyIDE3LjE1Mi0yMS4yNDgtMzIuNTEyLTkuNzI4LTQ0LjgtMzAuMjA4LTQ0LjgtMzAuMjA4IDMuNzY2IDIuNjM2IDkuOTc2IDYuMDUzIDEwLjQ5NiA2LjQgNDMuMjEgMjQuMTk4IDEwNC41ODggMzIuMTI2IDE1OS43NDQgOC45NiA4Ljk2LTMuMzI4IDE4Ljk0NC04LjE5MiAyOS40NC0xNS4xMDQgMCAwLTEyLjggMjAuOTkyLTQ2LjMzNiAzMC40NjQgNy42OCA5LjcyOCAxNi44OTYgMjAuNzM2IDE2Ljg5NiAyMC43MzYgNTYuNTc2LTEuNzkyIDc4LjMzNi0zOC45MTIgNzguMzM2LTM4LjkxMnoiPjwvcGF0aD48L3N2Zz4NCg==" />
						<span class="title">  Serveur Discord du Bus Magique</span>
					</a>
				</li>
				<li>
					<a href="https://outils.lebusmagique.fr/carte-interactive/" target="_blank">
						<img src="data:image/svg+xml;base64,PHN2ZyBhcmlhLWhpZGRlbj0idHJ1ZSIgZm9jdXNhYmxlPSJmYWxzZSIgZGF0YS1wcmVmaXg9ImZhciIgZGF0YS1pY29uPSJtYXAiIGNsYXNzPSJzdmctaW5saW5lLS1mYSBmYS1tYXAgZmEtdy0xOCIgcm9sZT0iaW1nIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA1NzYgNTEyIj48cGF0aCBmaWxsPSIjZmZmZmZmIiBkPSJNNTYwLjAyIDMyYy0xLjk2IDAtMy45OC4zNy01Ljk2IDEuMTZMMzg0LjAxIDk2SDM4NEwyMTIgMzUuMjhBNjQuMjUyIDY0LjI1MiAwIDAgMCAxOTEuNzYgMzJjLTYuNjkgMC0xMy4zNyAxLjA1LTE5LjgxIDMuMTRMMjAuMTIgODcuOTVBMzIuMDA2IDMyLjAwNiAwIDAgMCAwIDExNy42NnYzNDYuMzJDMCA0NzMuMTcgNy41MyA0ODAgMTUuOTkgNDgwYzEuOTYgMCAzLjk3LS4zNyA1Ljk2LTEuMTZMMTkyIDQxNmwxNzIgNjAuNzFhNjMuOTggNjMuOTggMCAwIDAgNDAuMDUuMTVsMTUxLjgzLTUyLjgxQTMxLjk5NiAzMS45OTYgMCAwIDAgNTc2IDM5NC4zNFY0OC4wMmMwLTkuMTktNy41My0xNi4wMi0xNS45OC0xNi4wMnpNMjI0IDkwLjQybDEyOCA0NS4xOXYyODUuOTdsLTEyOC00NS4xOVY5MC40MnpNNDggNDE4LjA1VjEyOS4wN2wxMjgtNDQuNTN2Mjg2LjJsLS42NC4yM0w0OCA0MTguMDV6bTQ4MC0zNS4xM2wtMTI4IDQ0LjUzVjE0MS4yNmwuNjQtLjI0TDUyOCA5My45NXYyODguOTd6Ij48L3BhdGg+PC9zdmc+DQo=" />
						<span class="title">Carte interactive</span>
					</a>
				</li>
				<li class="high">
					<a href="https://www.lebusmagique.fr/pages/infos/comment-nous-rejoindre.html" target="_blank">
					  <img src="data:image/svg+xml;base64,PHN2ZyBhcmlhLWhpZGRlbj0idHJ1ZSIgZm9jdXNhYmxlPSJmYWxzZSIgZGF0YS1wcmVmaXg9ImZhcyIgZGF0YS1pY29uPSJidXMiIGNsYXNzPSJzdmctaW5saW5lLS1mYSBmYS1idXMgZmEtdy0xNiIgcm9sZT0iaW1nIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA1MTIgNTEyIj48cGF0aCBmaWxsPSIjZmZmZmZmIiBkPSJNNDg4IDEyOGgtOFY4MGMwLTQ0LjgtOTkuMi04MC0yMjQtODBTMzIgMzUuMiAzMiA4MHY0OGgtOGMtMTMuMjUgMC0yNCAxMC43NC0yNCAyNHY4MGMwIDEzLjI1IDEwLjc1IDI0IDI0IDI0aDh2MTYwYzAgMTcuNjcgMTQuMzMgMzIgMzIgMzJ2MzJjMCAxNy42NyAxNC4zMyAzMiAzMiAzMmgzMmMxNy42NyAwIDMyLTE0LjMzIDMyLTMydi0zMmgxOTJ2MzJjMCAxNy42NyAxNC4zMyAzMiAzMiAzMmgzMmMxNy42NyAwIDMyLTE0LjMzIDMyLTMydi0zMmg2LjRjMTYgMCAyNS42LTEyLjggMjUuNi0yNS42VjI1Nmg4YzEzLjI1IDAgMjQtMTAuNzUgMjQtMjR2LTgwYzAtMTMuMjYtMTAuNzUtMjQtMjQtMjR6TTExMiA0MDBjLTE3LjY3IDAtMzItMTQuMzMtMzItMzJzMTQuMzMtMzIgMzItMzIgMzIgMTQuMzMgMzIgMzItMTQuMzMgMzItMzIgMzJ6bTE2LTExMmMtMTcuNjcgMC0zMi0xNC4zMy0zMi0zMlYxMjhjMC0xNy42NyAxNC4zMy0zMiAzMi0zMmgyNTZjMTcuNjcgMCAzMiAxNC4zMyAzMiAzMnYxMjhjMCAxNy42Ny0xNC4zMyAzMi0zMiAzMkgxMjh6bTI3MiAxMTJjLTE3LjY3IDAtMzItMTQuMzMtMzItMzJzMTQuMzMtMzIgMzItMzIgMzIgMTQuMzMgMzIgMzItMTQuMzMgMzItMzIgMzJ6Ij48L3BhdGg+PC9zdmc+DQo="/>
						<span class="title">Rejoignez la communauté</span>
						<span class="subtitle">Envie de monter à bord du Bus&nbsp;?</span>
					</a>
				</li>
				<li>
					<a href="https://www.lebusmagique.fr/pages/outils-gw2/banque-de-materiaux-et-portefeuille.html" target="_blank">
					  <img src="data:image/svg+xml;base64,PHN2ZyBhcmlhLWhpZGRlbj0idHJ1ZSIgZm9jdXNhYmxlPSJmYWxzZSIgZGF0YS1wcmVmaXg9ImZhcyIgZGF0YS1pY29uPSJwaWdneS1iYW5rIiBjbGFzcz0ic3ZnLWlubGluZS0tZmEgZmEtcGlnZ3ktYmFuayBmYS13LTE4IiByb2xlPSJpbWciIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgdmlld0JveD0iMCAwIDU3NiA1MTIiPjxwYXRoIGZpbGw9IiNmZmZmZmYiIGQ9Ik01NjAgMjI0aC0yOS41Yy04LjgtMjAtMjEuNi0zNy43LTM3LjQtNTIuNUw1MTIgOTZoLTMyYy0yOS40IDAtNTUuNCAxMy41LTczIDM0LjMtNy42LTEuMS0xNS4xLTIuMy0yMy0yLjNIMjU2Yy03Ny40IDAtMTQxLjkgNTUtMTU2LjggMTI4SDU2Yy0xNC44IDAtMjYuNS0xMy41LTIzLjUtMjguOEMzNC43IDIxNS44IDQ1LjQgMjA4IDU3IDIwOGgxYzMuMyAwIDYtMi43IDYtNnYtMjBjMC0zLjMtMi43LTYtNi02LTI4LjUgMC01My45IDIwLjQtNTcuNSA0OC42Qy0zLjkgMjU4LjggMjIuNyAyODggNTYgMjg4aDQwYzAgNTIuMiAyNS40IDk4LjEgNjQgMTI3LjNWNDk2YzAgOC44IDcuMiAxNiAxNiAxNmg2NGM4LjggMCAxNi03LjIgMTYtMTZ2LTQ4aDEyOHY0OGMwIDguOCA3LjIgMTYgMTYgMTZoNjRjOC44IDAgMTYtNy4yIDE2LTE2di04MC43YzExLjgtOC45IDIyLjMtMTkuNCAzMS4zLTMxLjNINTYwYzguOCAwIDE2LTcuMiAxNi0xNlYyNDBjMC04LjgtNy4yLTE2LTE2LTE2em0tMTI4IDY0Yy04LjggMC0xNi03LjItMTYtMTZzNy4yLTE2IDE2LTE2IDE2IDcuMiAxNiAxNi03LjIgMTYtMTYgMTZ6TTI1NiA5NmgxMjhjNS40IDAgMTAuNy40IDE1LjkuOCAwLS4zLjEtLjUuMS0uOCAwLTUzLTQzLTk2LTk2LTk2cy05NiA0My05NiA5NmMwIDIuMS41IDQuMS42IDYuMiAxNS4yLTMuOSAzMS02LjIgNDcuNC02LjJ6Ij48L3BhdGg+PC9zdmc+DQo=" />
						<span class="title">Banque de matériaux & portefeuille</span>
					</a>
				</li>
				<li>
					<a href="https://www.lebusmagique.fr/pages/guides/home/l-instance-personnelle.html" target="_blank">
					  <img src="data:image/svg+xml;base64,PHN2ZyBhcmlhLWhpZGRlbj0idHJ1ZSIgZm9jdXNhYmxlPSJmYWxzZSIgZGF0YS1wcmVmaXg9ImZhcyIgZGF0YS1pY29uPSJob21lIiBjbGFzcz0ic3ZnLWlubGluZS0tZmEgZmEtaG9tZSBmYS13LTE4IiByb2xlPSJpbWciIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgdmlld0JveD0iMCAwIDU3NiA1MTIiPjxwYXRoIGZpbGw9IiNmZmZmZmYiIGQ9Ik0yODAuMzcgMTQ4LjI2TDk2IDMwMC4xMVY0NjRhMTYgMTYgMCAwIDAgMTYgMTZsMTEyLjA2LS4yOWExNiAxNiAwIDAgMCAxNS45Mi0xNlYzNjhhMTYgMTYgMCAwIDEgMTYtMTZoNjRhMTYgMTYgMCAwIDEgMTYgMTZ2OTUuNjRhMTYgMTYgMCAwIDAgMTYgMTYuMDVMNDY0IDQ4MGExNiAxNiAwIDAgMCAxNi0xNlYzMDBMMjk1LjY3IDE0OC4yNmExMi4xOSAxMi4xOSAwIDAgMC0xNS4zIDB6TTU3MS42IDI1MS40N0w0ODggMTgyLjU2VjQ0LjA1YTEyIDEyIDAgMCAwLTEyLTEyaC01NmExMiAxMiAwIDAgMC0xMiAxMnY3Mi42MUwzMTguNDcgNDNhNDggNDggMCAwIDAtNjEgMEw0LjM0IDI1MS40N2ExMiAxMiAwIDAgMC0xLjYgMTYuOWwyNS41IDMxQTEyIDEyIDAgMCAwIDQ1LjE1IDMwMWwyMzUuMjItMTkzLjc0YTEyLjE5IDEyLjE5IDAgMCAxIDE1LjMgMEw1MzAuOSAzMDFhMTIgMTIgMCAwIDAgMTYuOS0xLjZsMjUuNS0zMWExMiAxMiAwIDAgMC0xLjctMTYuOTN6Ij48L3BhdGg+PC9zdmc+DQo=" />
						<span class="title">Instance personnelle</span>
						<span class="subtitle">Améliorez votre zone personnelle</span>
					</a>
				</li>
				<li>
					<a href="https://outils.lebusmagique.fr/observatory/" target="_blank">
					  <img src="data:image/svg+xml;base64,PHN2ZyBhcmlhLWhpZGRlbj0idHJ1ZSIgZm9jdXNhYmxlPSJmYWxzZSIgZGF0YS1wcmVmaXg9ImZhcyIgZGF0YS1pY29uPSJoaXN0b3J5IiBjbGFzcz0ic3ZnLWlubGluZS0tZmEgZmEtaGlzdG9yeSBmYS13LTE2IiByb2xlPSJpbWciIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgdmlld0JveD0iMCAwIDUxMiA1MTIiPjxwYXRoIGZpbGw9IiNmZmZmZmYiIGQ9Ik01MDQgMjU1LjUzMWMuMjUzIDEzNi42NC0xMTEuMTggMjQ4LjM3Mi0yNDcuODIgMjQ4LjQ2OC01OS4wMTUuMDQyLTExMy4yMjMtMjAuNTMtMTU1LjgyMi01NC45MTEtMTEuMDc3LTguOTQtMTEuOTA1LTI1LjU0MS0xLjgzOS0zNS42MDdsMTEuMjY3LTExLjI2N2M4LjYwOS04LjYwOSAyMi4zNTMtOS41NTEgMzEuODkxLTEuOTg0QzE3My4wNjIgNDI1LjEzNSAyMTIuNzgxIDQ0MCAyNTYgNDQwYzEwMS43MDUgMCAxODQtODIuMzExIDE4NC0xODQgMC0xMDEuNzA1LTgyLjMxMS0xODQtMTg0LTE4NC00OC44MTQgMC05My4xNDkgMTguOTY5LTEyNi4wNjggNDkuOTMybDUwLjc1NCA1MC43NTRjMTAuMDggMTAuMDggMi45NDEgMjcuMzE0LTExLjMxMyAyNy4zMTRIMjRjLTguODM3IDAtMTYtNy4xNjMtMTYtMTZWMzguNjI3YzAtMTQuMjU0IDE3LjIzNC0yMS4zOTMgMjcuMzE0LTExLjMxNGw0OS4zNzIgNDkuMzcyQzEyOS4yMDkgMzQuMTM2IDE4OS41NTIgOCAyNTYgOGMxMzYuODEgMCAyNDcuNzQ3IDExMC43OCAyNDggMjQ3LjUzMXptLTE4MC45MTIgNzguNzg0bDkuODIzLTEyLjYzYzguMTM4LTEwLjQ2MyA2LjI1My0yNS41NDItNC4yMS0zMy42NzlMMjg4IDI1Ni4zNDlWMTUyYzAtMTMuMjU1LTEwLjc0NS0yNC0yNC0yNGgtMTZjLTEzLjI1NSAwLTI0IDEwLjc0NS0yNCAyNHYxMzUuNjUxbDY1LjQwOSA1MC44NzRjMTAuNDYzIDguMTM3IDI1LjU0MSA2LjI1MyAzMy42NzktNC4yMXoiPjwvcGF0aD48L3N2Zz4NCg==" />
						<span class="title">GW2 Observatory</span>
						<span class="subtitle">Remontez la chronologie de vos personnages</span>
					</a>
				</li>
				<li class="large">
					<a href="https://www.lebusmagique.fr/pages/outils-gw2/decorations-de-hall-de-guilde.html" target="_blank">
					  <img src="data:image/svg+xml;base64,PHN2ZyBhcmlhLWhpZGRlbj0idHJ1ZSIgZm9jdXNhYmxlPSJmYWxzZSIgZGF0YS1wcmVmaXg9ImZhcyIgZGF0YS1pY29uPSJwdXp6bGUtcGllY2UiIGNsYXNzPSJzdmctaW5saW5lLS1mYSBmYS1wdXp6bGUtcGllY2UgZmEtdy0xOCIgcm9sZT0iaW1nIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA1NzYgNTEyIj48cGF0aCBmaWxsPSIjZmZmZmZmIiBkPSJNNTE5LjQ0MiAyODguNjUxYy00MS41MTkgMC01OS41IDMxLjU5My04Mi4wNTggMzEuNTkzQzM3Ny40MDkgMzIwLjI0NCA0MzIgMTQ0IDQzMiAxNDRzLTE5Ni4yODggODAtMTk2LjI4OC0zLjI5N2MwLTM1LjgyNyAzNi4yODgtNDYuMjUgMzYuMjg4LTg1Ljk4NUMyNzIgMTkuMjE2IDI0My44ODUgMCAyMTAuNTM5IDBjLTM0LjY1NCAwLTY2LjM2NiAxOC44OTEtNjYuMzY2IDU2LjM0NiAwIDQxLjM2NCAzMS43MTEgNTkuMjc3IDMxLjcxMSA4MS43NUMxNzUuODg1IDIwNy43MTkgMCAxNjYuNzU4IDAgMTY2Ljc1OHYzMzMuMjM3czE3OC42MzUgNDEuMDQ3IDE3OC42MzUtMjguNjYyYzAtMjIuNDczLTQwLTQwLjEwNy00MC04MS40NzEgMC0zNy40NTYgMjkuMjUtNTYuMzQ2IDYzLjU3Ny01Ni4zNDYgMzMuNjczIDAgNjEuNzg4IDE5LjIxNiA2MS43ODggNTQuNzE3IDAgMzkuNzM1LTM2LjI4OCA1MC4xNTgtMzYuMjg4IDg1Ljk4NSAwIDYwLjgwMyAxMjkuNjc1IDI1LjczIDE4MS4yMyAyNS43MyAwIDAtMzQuNzI1LTEyMC4xMDEgMjUuODI3LTEyMC4xMDEgMzUuOTYyIDAgNDYuNDIzIDM2LjE1MiA4Ni4zMDggMzYuMTUyQzU1Ni43MTIgNDE2IDU3NiAzODcuOTkgNTc2IDM1NC40NDNjMC0zNC4xOTktMTguOTYyLTY1Ljc5Mi01Ni41NTgtNjUuNzkyeiI+PC9wYXRoPjwvc3ZnPg0K" />
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

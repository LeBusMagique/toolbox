<svelte:options tag="lbm-toolbar" accessors={false} />

<script>
	let show = false;

	function toggleToolbar() {
		show = !show;
	}
</script>

<style>
	a#button {
		position: fixed;
		top: 10%;
		left: 0;
		z-index: 10001;
		width: 3em;
		height: 3em;
		display: flex;
		border-radius: 0 4px 4px 0;
		border: 0;
		background: #fff;
		box-shadow: 0 0 10px rgba(0, 0, 0, .5);
		padding: 0;
		cursor: pointer;
		align-items: center;
		justify-content: center;
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
	}

	#wrap {
		display: flex;
		align-items: center;
		justify-content: center;
		height: 100%;
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
		background: red;
		border-radius: 4px;
	}

	#tools li a span {
		display: block;
		width: 100%;
		text-align: center;
	}

	#tools li a .subtitle {
		font-weight: normal;
		font-size: .8em;
	}
</style>

<a on:click="{toggleToolbar}" id="button">
	{#if show}
		&times;
	{:else}
		LBM
	{/if}
</a>

<p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Fugit est fugiat eaque, deleniti ducimus ut autem quibusdam ab voluptatibus optio nemo nulla? Repellat iste ab rem, quia doloremque reiciendis saepe!</p>
<p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Fugit est fugiat eaque, deleniti ducimus ut autem quibusdam ab voluptatibus optio nemo nulla? Repellat iste ab rem, quia doloremque reiciendis saepe!</p>
<p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Fugit est fugiat eaque, deleniti ducimus ut autem quibusdam ab voluptatibus optio nemo nulla? Repellat iste ab rem, quia doloremque reiciendis saepe!</p>
<p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Fugit est fugiat eaque, deleniti ducimus ut autem quibusdam ab voluptatibus optio nemo nulla? Repellat iste ab rem, quia doloremque reiciendis saepe!</p>
<p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Fugit est fugiat eaque, deleniti ducimus ut autem quibusdam ab voluptatibus optio nemo nulla? Repellat iste ab rem, quia doloremque reiciendis saepe!</p>
<p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Fugit est fugiat eaque, deleniti ducimus ut autem quibusdam ab voluptatibus optio nemo nulla? Repellat iste ab rem, quia doloremque reiciendis saepe!</p>
<p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Fugit est fugiat eaque, deleniti ducimus ut autem quibusdam ab voluptatibus optio nemo nulla? Repellat iste ab rem, quia doloremque reiciendis saepe!</p>
<p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Fugit est fugiat eaque, deleniti ducimus ut autem quibusdam ab voluptatibus optio nemo nulla? Repellat iste ab rem, quia doloremque reiciendis saepe!</p>
<p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Fugit est fugiat eaque, deleniti ducimus ut autem quibusdam ab voluptatibus optio nemo nulla? Repellat iste ab rem, quia doloremque reiciendis saepe!</p>
<p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Fugit est fugiat eaque, deleniti ducimus ut autem quibusdam ab voluptatibus optio nemo nulla? Repellat iste ab rem, quia doloremque reiciendis saepe!</p>
<p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Fugit est fugiat eaque, deleniti ducimus ut autem quibusdam ab voluptatibus optio nemo nulla? Repellat iste ab rem, quia doloremque reiciendis saepe!</p>
<p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Fugit est fugiat eaque, deleniti ducimus ut autem quibusdam ab voluptatibus optio nemo nulla? Repellat iste ab rem, quia doloremque reiciendis saepe!</p>
<p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Fugit est fugiat eaque, deleniti ducimus ut autem quibusdam ab voluptatibus optio nemo nulla? Repellat iste ab rem, quia doloremque reiciendis saepe!</p>
<p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Fugit est fugiat eaque, deleniti ducimus ut autem quibusdam ab voluptatibus optio nemo nulla? Repellat iste ab rem, quia doloremque reiciendis saepe!</p>
<p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Fugit est fugiat eaque, deleniti ducimus ut autem quibusdam ab voluptatibus optio nemo nulla? Repellat iste ab rem, quia doloremque reiciendis saepe!</p>
<p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Fugit est fugiat eaque, deleniti ducimus ut autem quibusdam ab voluptatibus optio nemo nulla? Repellat iste ab rem, quia doloremque reiciendis saepe!</p>
<p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Fugit est fugiat eaque, deleniti ducimus ut autem quibusdam ab voluptatibus optio nemo nulla? Repellat iste ab rem, quia doloremque reiciendis saepe!</p>
<p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Fugit est fugiat eaque, deleniti ducimus ut autem quibusdam ab voluptatibus optio nemo nulla? Repellat iste ab rem, quia doloremque reiciendis saepe!</p>

{#if show}
	<div id="overlay">
		<div id="wrap">
			<ul id="tools">
				<li class="large"><a href="#!" target="_blank"><span class="title">Site principal</span></a></li>
				<li><a href="#!" target="_blank"><span class="title">Outil 1</span></a></li>
				<li class="high">
					<a href="#!" target="_blank">
						<span class="title">Outil 3</span>
						<span class="subtitle">Subtitle</span>
					</a>
				</li>
				<li><a href="#!" target="_blank"><span class="title">Outil 2</span></a></li>
				<li class="high">
					<a href="#!" target="_blank">
						<span class="title">Outil 4</span>
						<span class="subtitle">Subtitle</span>
					</a>
				</li>
				<li><a href="#!" target="_blank"><span class="title">Outil 5</span></a></li>
				<li><a href="#!" target="_blank"><span class="title">Outil 6</span></a></li>
				<li><a href="#!" target="_blank"><span class="title">Outil 7</span></a></li>
				<li><a href="#!" target="_blank"><span class="title">Outil 8</span></a></li>
				<li class="large"><a href="#!" target="_blank"><span class="title">RSS</span></a></li>
			</ul>
		</div>
	</div>
{/if}

<!-- Card de imagen -->
<script lang="ts">
	// Creamos una interfaz para definir el tipo de dato de las imágenes
	interface ImageData {
		url: string;
		descripcion: string;
		precio: number;
	}

	// Array de imágenes con URL, descripción y precio
	const imageUrl = 'https://source.unsplash.com/random/200x200?sig=incrementingIdentifier';
	let arrayImgRandom: ImageData[] = [];
	for (let i = 0; i < 10; i++) {
		arrayImgRandom.push({
			url: imageUrl,
			descripcion: `Producto ${i + 1}`,
			precio: (i + 1) * 10 // Precio ficticio basado en el índice (1 * 10, 2 * 10, etc.)
		});
	}
</script>

<!-- Creamos la cardcita :)) -->
<div class="container mx-auto p-8">
	<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
		{#each arrayImgRandom as img (img.url)}
			<div class="bg-white rounded-lg shadow-md p-4">
				<img src={img.url} alt={img.descripcion} class="w-full h-40 object-cover mb-4" />
				<p class="text-gray-700 font-semibold">{img.descripcion}</p>
				<p class="text-gray-600">Precio: ${img.precio}</p>
				<button class="bg-red-300 rounded-md p-2">Agregar al carrito</button>
			</div>
		{/each}
	</div>
</div>

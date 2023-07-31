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
	for (let i = 0; i < 3; i++) {
		arrayImgRandom.push({
			url: imageUrl,
			descripcion: `Producto ${i + 1}`,
			precio: (i + 1) * 10 // Precio ficticio basado en el índice (1 * 10, 2 * 10, etc.)
		});
	}
</script>

<div class="container mx-auto p-8">
    <div class="flex flex-wrap -mx-4">
        {#each arrayImgRandom as img (img.url)}
            <div class="w-full md:w-1/2 lg:w-1/3 px-4 mb-4">
                <div class="bg-white rounded-lg shadow-md p-4 flex flex-col items-center">
                    <img src={img.url} alt={img.descripcion} class="w-full h-40 object-cover mb-4" />
                    <p class="text-gray-700 font-semibold text-center">{img.descripcion}</p>
                    <p class="text-gray-600 text-center">Precio: ${img.precio}</p>
                    <button class="bg-red-300 rounded-md p-2">Agregar al carrito</button>
                </div>
            </div>
        {/each}
    </div>
</div>
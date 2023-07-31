<script lang="ts">
	// creamos una interfaz para definir el tipo de dato de los productos
	interface Producto {
	  id: number;
	  nombre: string;
	  imagen: string;
	  precio: number;
	  cantidad: number;
	}
	
	// tipamos el carrito como un array de productos
	let cart: Producto[] = [];
	
	// creamos un array de productos
	let products: Producto[] = [
	{ id: 1, nombre: "Manzana", imagen: "https://www.applesfromny.com/wp-content/uploads/2020/05/Jonagold_NYAS-Apples2.png", precio: 10, cantidad: 1 },
	{ id: 2, nombre: "Naranja", imagen: "https://5.imimg.com/data5/VN/YP/MY-33296037/orange-600x600-500x500.jpg", precio: 11, cantidad: 1 },
	{ id: 3, nombre: "Uva", imagen: "https://www.aicr.org/wp-content/uploads/2020/01/shutterstock_533487490-640x462.jpg", precio: 12, cantidad: 1 },
	];
	
	// creamos una función para agregar productos al carrito
	const anhadirAlcarrito = (product: Producto): void => {
	for (let item of cart) {
	if (item.id === product.id) {
		item.cantidad += 1;
		updateCart();
		return;
	}
	}
	cart = [...cart, product];
	updateCart();
	};
	
	// creamos una función para actualizar el carrito cada vez que se agregue un producto o se modifique la cantidad
	const updateCart = (): void => {
	  total = cart.reduce((sum, item) => sum + item.precio * item.cantidad, 0);
	};
	
	const actualizarCantidad = (item: Producto, action: 'minus' | 'plus'): void => {
	if (action === 'minus') {
	if (item.cantidad > 1) {
		item.cantidad -= 1;
	} else {
		cart = cart.filter((cartItem) => cartItem !== item);
	}
	} else if (action === 'plus') {
	item.cantidad += 1;
	}
	updateCart();
};

let total: number = cart.reduce((sum, item) => sum + item.precio * item.cantidad, 0);
</script>

<div class="grid grid-cols-3 gap-4">
	{#each products as product}
	<div class="border p-4">
		<div class="h-32 bg-center bg-no-repeat bg-contain" style="background-image: url({product.imagen})"></div>
		<h4 class="text-xl font-bold">{product.nombre}</h4>
		<p class="text-lg">${product.precio}</p>
		<button class="mt-2 px-4 py-2 bg-blue-500 text-white rounded" on:click={() => anhadirAlcarrito(product)}>Add to cart</button>
	</div>
	{/each}
</div>

<div class="border p-4 mt-4">
	<p class="text-center">Tienes {cart.length} tipo/s de producto/s en tu carrito</p>
	{#each cart as item }
	{#if item.cantidad > 0}
	<div class="flex items-center justify-between mb-2">
	<img class="w-12 h-12 object-cover" src={item.imagen} alt={item.nombre}/>
	<div class="flex items-center">
		<button class="px-2 py-1 bg-blue-500 text-white rounded-l" on:click={() => actualizarCantidad(item, 'minus')}>-</button>
		<span class="px-4 py-2 bg-gray-200">{item.cantidad}</span>
		<button class="px-2 py-1 bg-blue-500 text-white rounded-r" on:click={() => actualizarCantidad(item, 'plus')}>+</button>
	</div>
	<p class="text-lg">${item.precio * item.cantidad}</p>
	</div>
	{/if}
	{/each}
	<div class="text-right">
	<h4 class="text-2xl font-bold">Total: $ {total}</h4>
	<button class="mt-2 px-4 py-2 bg-blue-500 text-white rounded">limpiar carrito</button>
	</div>
	</div>
	
/* ============================================================
   SUDOR Y GLORIA - JAVASCRIPT
   Carrito funcional, localStorage, modales, toast, etc.
   ============================================================ */

// ----- DATOS DE PRODUCTOS -----
const productos = [
    {
        id: 1,
        nombre: 'Camiseta Dry-Fit',
        descripcion: 'Mangas cortas, tejido ligero que absorbe sudor. Ideal para running y pesas.',
        precio: 89.00,
        imagen: 'https://images.unsplash.com/photo-1521572163474-6864f9cf17ab?w=600&h=800&fit=crop',
        colores: ['Negro', 'Gris', 'Azul Marino'],
        tallas: ['S', 'M', 'L', 'XL', 'XXL'],
        categoria: 'hombres',
        badge: 'Nuevo'
    },
    {
        id: 2,
        nombre: 'Tank Top Sin Mangas',
        descripcion: 'Corte anatómico, libre de costuras. Máxima libertad de movimiento.',
        precio: 79.00,
        imagen: 'https://images.unsplash.com/photo-1581655353564-df123a1eb820?w=600&h=800&fit=crop',
        colores: ['Negro', 'Rojo', 'Militar'],
        tallas: ['S', 'M', 'L', 'XL'],
        categoria: 'hombres',
        badge: ''
    },
    {
        id: 3,
        nombre: 'Leggings High Waist',
        descripcion: 'Tela suave, no se transparenta, bolsillo lateral. Perfecto para yoga y gym.',
        precio: 139.00,
        imagen: 'https://images.unsplash.com/photo-1506629082955-511b1aa562c8?w=600&h=800&fit=crop',
        colores: ['Negro', 'Rosa', 'Verde Menta'],
        tallas: ['XS', 'S', 'M', 'L', 'XL'],
        categoria: 'mujeres',
        badge: 'Popular'
    },
    {
        id: 4,
        nombre: 'Short de Compresión',
        descripcion: '2 en 1: interior ajustado + exterior suelto. Secado rápido.',
        precio: 129.00,
        imagen: 'https://images.unsplash.com/photo-1565693413579-8ff3fdc1b03b?w=600&h=800&fit=crop',
        colores: ['Negro', 'Carbón'],
        tallas: ['S', 'M', 'L', 'XL', 'XXL'],
        categoria: 'hombres',
        badge: ''
    },
    {
        id: 5,
        nombre: 'Joggers Deportivos',
        descripcion: 'Algodón + poliéster, bolsillos con cierre. Comodidad total.',
        precio: 159.00,
        imagen: 'https://images.unsplash.com/photo-1517438324-91e22aa6b07c?w=600&h=800&fit=crop',
        colores: ['Negro', 'Gris', 'Oliva'],
        tallas: ['M', 'L', 'XL', 'XXL'],
        categoria: 'hombres',
        badge: ''
    },
    {
        id: 6,
        nombre: 'Top Deportivo',
        descripcion: 'Soporte medio, sujetador integrado. Ideal para yoga y pilates.',
        precio: 99.00,
        imagen: 'https://images.unsplash.com/photo-1518310383802-640c2de311b2?w=600&h=800&fit=crop',
        colores: ['Negro', 'Blanco', 'Lila'],
        tallas: ['XS', 'S', 'M', 'L'],
        categoria: 'mujeres',
        badge: ''
    },
    {
        id: 7,
        nombre: 'Sudadera con Capucha',
        descripcion: 'Felpa cepillada, cordones metálicos. Abrigo con estilo.',
        precio: 189.00,
        imagen: 'https://images.unsplash.com/photo-1556821840-3a63f95609a7?w=600&h=800&fit=crop',
        colores: ['Negro', 'Azul Noche'],
        tallas: ['S', 'M', 'L', 'XL'],
        categoria: 'hombres',
        badge: 'Premium'
    },
    {
        id: 8,
        nombre: 'Short Ciclista',
        descripcion: 'Talla ajustada, 5" de longitud. Libertad para cada movimiento.',
        precio: 89.00,
        imagen: 'https://images.unsplash.com/photo-1507398941213-5726e0cfe21e?w=600&h=800&fit=crop',
        colores: ['Negro', 'Burdeos'],
        tallas: ['XS', 'S', 'M', 'L'],
        categoria: 'mujeres',
        badge: ''
    }
];

// ----- ESTADO DEL CARRITO (persiste en localStorage) -----
let carrito = JSON.parse(localStorage.getItem('carritoSudorYGloria')) || [];

// ----- FUNCIONES DEL CARRITO -----
function guardarCarrito() {
    localStorage.setItem('carritoSudorYGloria', JSON.stringify(carrito));
    actualizarBadge();
}

function actualizarBadge() {
    const totalItems = carrito.reduce((acc, item) => acc + item.cantidad, 0);
    const badge = document.getElementById('cartBadge');
    badge.textContent = totalItems;
    // Animación de pulso
    badge.classList.add('pulse');
    setTimeout(() => badge.classList.remove('pulse'), 400);
}

function agregarAlCarrito(producto, color, talla) {
    const existente = carrito.find(
        item => item.id === producto.id && item.color === color && item.talla === talla
    );
    if (existente) {
        existente.cantidad += 1;
    } else {
        carrito.push({
            id: producto.id,
            nombre: producto.nombre,
            precio: producto.precio,
            imagen: producto.imagen,
            color: color,
            talla: talla,
            cantidad: 1
        });
    }
    guardarCarrito();
    mostrarToast(`"${producto.nombre}" agregado al carrito 🛒`, 'success');
}

function eliminarDelCarrito(index) {
    const eliminado = carrito[index];
    carrito.splice(index, 1);
    guardarCarrito();
    mostrarToast(`"${eliminado.nombre}" eliminado del carrito 🗑️`, 'error');
    renderizarCarrito();
}

function cambiarCantidad(index, nuevaCantidad) {
    if (nuevaCantidad < 1) {
        eliminarDelCarrito(index);
        return;
    }
    carrito[index].cantidad = nuevaCantidad;
    guardarCarrito();
    renderizarCarrito();
}

function calcularTotal() {
    return carrito.reduce((acc, item) => acc + item.precio * item.cantidad, 0);
}

function formatearPrecio(valor) {
    return `Q${valor.toFixed(2)}`;
}

// ----- TOAST NOTIFICATIONS -----
function mostrarToast(mensaje, tipo = 'success') {
    const container = document.getElementById('toastContainer');
    const toast = document.createElement('div');
    toast.className = `toast toast--${tipo}`;
    const iconos = {
        success: 'fa-circle-check',
        error: 'fa-circle-xmark'
    };
    toast.innerHTML = `<i class="fa-solid ${iconos[tipo] || iconos.success}"></i> ${mensaje}`;
    container.appendChild(toast);
    // Eliminar tras la animación
    setTimeout(() => {
        if (toast.parentNode) {
            toast.remove();
        }
    }, 3200);
}

// ----- RENDERIZAR CATÁLOGO -----
function renderizarCatalogo() {
    const grid = document.getElementById('catalogGrid');
    if (!grid) return;

    grid.innerHTML = productos.map(prod => {
        const opcionesColores = prod.colores.map(c => `<option value="${c}">${c}</option>`).join('');
        const opcionesTallas = prod.tallas.map(t => `<option value="${t}">${t}</option>`).join('');
        return `
            <div class="product-card" data-id="${prod.id}">
                <div class="product-card__img-wrapper">
                    <img src="${prod.imagen}" alt="${prod.nombre}" class="product-card__img" loading="lazy">
                    ${prod.badge ? `<span class="product-card__badge">${prod.badge}</span>` : ''}
                </div>
                <div class="product-card__body">
                    <h3 class="product-card__name">${prod.nombre}</h3>
                    <p class="product-card__desc">${prod.descripcion}</p>
                    <p class="product-card__price">${formatearPrecio(prod.precio)}</p>
                    <div class="product-card__options">
                        <select class="product-card__select color-select" aria-label="Color">
                            ${opcionesColores}
                        </select>
                        <select class="product-card__select talla-select" aria-label="Talla">
                            ${opcionesTallas}
                        </select>
                    </div>
                    <button class="product-card__btn add-to-cart-btn">
                        <i class="fa-solid fa-cart-plus"></i> Agregar al Carrito
                    </button>
                </div>
            </div>
        `;
    }).join('');

    // Asignar eventos a los botones "Agregar al carrito"
    grid.querySelectorAll('.add-to-cart-btn').forEach(btn => {
        btn.addEventListener('click', (e) => {
            const card = e.target.closest('.product-card');
            const id = parseInt(card.dataset.id);
            const colorSelect = card.querySelector('.color-select');
            const tallaSelect = card.querySelector('.talla-select');
            const producto = productos.find(p => p.id === id);
            if (producto) {
                agregarAlCarrito(producto, colorSelect.value, tallaSelect.value);
            }
        });
    });
}

// ----- RENDERIZAR CARRITO EN MODAL -----
function renderizarCarrito() {
    const container = document.getElementById('cartItemsContainer');
    const footer = document.getElementById('cartFooter');
    const totalEl = document.getElementById('cartTotal');

    if (carrito.length === 0) {
        container.innerHTML = '<p class="cart-empty">Tu carrito está vacío. ¡Agregá productos!</p>';
        footer.style.display = 'none';
    } else {
        container.innerHTML = carrito.map((item, index) => `
            <div class="cart-item">
                <img src="${item.imagen}" alt="${item.nombre}" class="cart-item__img">
                <div class="cart-item__info">
                    <p class="cart-item__name">${item.nombre}</p>
                    <p class="cart-item__variant">${item.color} / Talla ${item.talla}</p>
                    <p class="cart-item__price">${formatearPrecio(item.precio)} c/u</p>
                </div>
                <div class="cart-item__actions">
                    <button class="btn-icon btn-sm cart-qty-dec" data-index="${index}" aria-label="Reducir cantidad">−</button>
                    <input type="number" class="cart-item__qty" value="${item.cantidad}" min="1" data-index="${index}" readonly>
                    <button class="btn-icon btn-sm cart-qty-inc" data-index="${index}" aria-label="Aumentar cantidad">+</button>
                    <button class="btn-icon btn-sm cart-item__remove" data-index="${index}" aria-label="Eliminar producto">
                        <i class="fa-solid fa-trash-can"></i>
                    </button>
                </div>
            </div>
        `).join('');
        footer.style.display = 'block';
        totalEl.textContent = formatearPrecio(calcularTotal());
    }

    // Eventos de cantidad y eliminar
    container.querySelectorAll('.cart-qty-inc').forEach(btn => {
        btn.addEventListener('click', () => {
            const index = parseInt(btn.dataset.index);
            cambiarCantidad(index, carrito[index].cantidad + 1);
        });
    });
    container.querySelectorAll('.cart-qty-dec').forEach(btn => {
        btn.addEventListener('click', () => {
            const index = parseInt(btn.dataset.index);
            cambiarCantidad(index, carrito[index].cantidad - 1);
        });
    });
    container.querySelectorAll('.cart-item__remove').forEach(btn => {
        btn.addEventListener('click', () => {
            const index = parseInt(btn.dataset.index);
            eliminarDelCarrito(index);
        });
    });
}

// ----- MODALES -----
function abrirModal(overlayId) {
    const overlay = document.getElementById(overlayId);
    overlay.classList.add('active');
    document.body.style.overflow = 'hidden';
}

function cerrarModal(overlayId) {
    const overlay = document.getElementById(overlayId);
    overlay.classList.remove('active');
    document.body.style.overflow = '';
}

function cerrarTodosLosModales() {
    document.querySelectorAll('.modal-overlay').forEach(ov => ov.classList.remove('active'));
    document.body.style.overflow = '';
}

// ----- RENDERIZAR CHECKOUT SUMMARY -----
function renderizarCheckoutSummary() {
    const summary = document.getElementById('checkoutSummary');
    if (!summary) return;
    const subtotal = calcularTotal();
    const envio = subtotal >= 350 ? 0 : 35;
    const total = subtotal + envio;

    summary.innerHTML = `
        <h4>Resumen del Pedido</h4>
        ${carrito.map(item => `
            <div class="checkout-summary__item">
                <span>${item.nombre} (${item.cantidad}x) - ${item.color} / ${item.talla}</span>
                <span>${formatearPrecio(item.precio * item.cantidad)}</span>
            </div>
        `).join('')}
        <div class="checkout-summary__item">
            <span>Envío</span>
            <span>${envio === 0 ? 'GRATIS 🎉' : formatearPrecio(envio)}</span>
        </div>
        <div class="checkout-summary__total">
            <span>Total</span>
            <span>${formatearPrecio(total)}</span>
        </div>
        ${envio > 0 ? '<p style="font-size:0.8rem;color:var(--color-text-muted);margin-top:6px;">Agregá Q' + formatearPrecio(350 - subtotal) + ' más para envío gratis</p>' : ''}
    `;
}

// ----- EVENTOS PRINCIPALES AL CARGAR LA PÁGINA -----
document.addEventListener('DOMContentLoaded', () => {
    // Renderizar catálogo
    renderizarCatalogo();
    // Actualizar badge del carrito
    actualizarBadge();
    // Renderizar carrito inicial
    renderizarCarrito();

    // ----- BOTÓN CARRITO (abrir modal) -----
    document.getElementById('cartBtn').addEventListener('click', () => {
        renderizarCarrito();
        abrirModal('cartModalOverlay');
    });

    // ----- CERRAR MODAL CARRITO -----
    document.getElementById('closeCartModal').addEventListener('click', () => {
        cerrarModal('cartModalOverlay');
    });
    document.getElementById('cartModalOverlay').addEventListener('click', (e) => {
        if (e.target === e.currentTarget) cerrarModal('cartModalOverlay');
    });

    // ----- BOTÓN "CONTINUAR COMPRA" -----
    document.getElementById('checkoutBtn').addEventListener('click', () => {
        if (carrito.length === 0) {
            mostrarToast('El carrito está vacío 😕', 'error');
            return;
        }
        cerrarModal('cartModalOverlay');
        renderizarCheckoutSummary();
        abrirModal('checkoutModalOverlay');
    });

    // ----- CERRAR MODAL CHECKOUT -----
    document.getElementById('closeCheckoutModal').addEventListener('click', () => {
        cerrarModal('checkoutModalOverlay');
    });
    document.getElementById('checkoutModalOverlay').addEventListener('click', (e) => {
        if (e.target === e.currentTarget) cerrarModal('checkoutModalOverlay');
    });

    // ----- FORMULARIO CHECKOUT (simulado) -----
    document.getElementById('checkoutForm').addEventListener('submit', (e) => {
        e.preventDefault();
        // Simulación: siempre acepta los datos
        mostrarToast('✅ ¡Pedido confirmado con éxito! Te enviaremos un correo con los detalles.', 'success');
        // Vaciar carrito
        carrito = [];
        guardarCarrito();
        renderizarCarrito();
        // Cerrar modal de checkout
        cerrarModal('checkoutModalOverlay');
        // Scroll al inicio
        window.scrollTo({ top: 0, behavior: 'smooth' });
    });

    // ----- FORMULARIO DE CONTACTO (simulado) -----
    document.getElementById('contactForm').addEventListener('submit', (e) => {
        e.preventDefault();
        mostrarToast('📩 Consulta enviada con éxito. Te responderemos pronto.', 'success');
        e.target.reset();
    });

    // ----- FORMULARIO NEWSLETTER (simulado) -----
    document.getElementById('newsletterForm').addEventListener('submit', (e) => {
        e.preventDefault();
        mostrarToast('📬 ¡Suscripción exitosa! Bienvenido/a a la comunidad.', 'success');
        e.target.reset();
    });

    // ----- MENÚ HAMBURGUESA RESPONSIVE -----
    const hamburgerBtn = document.getElementById('hamburgerBtn');
    const mainNav = document.getElementById('mainNav');
    hamburgerBtn.addEventListener('click', () => {
        mainNav.classList.toggle('active');
        const icon = hamburgerBtn.querySelector('i');
        if (mainNav.classList.contains('active')) {
            icon.className = 'fa-solid fa-xmark';
        } else {
            icon.className = 'fa-solid fa-bars';
        }
    });

    // Cerrar menú al hacer clic en un enlace
    mainNav.querySelectorAll('.header__nav-link').forEach(link => {
        link.addEventListener('click', () => {
            mainNav.classList.remove('active');
            hamburgerBtn.querySelector('i').className = 'fa-solid fa-bars';
        });
    });

    // ----- ACTUALIZAR LINK ACTIVO EN NAVEGACIÓN AL HACER SCROLL -----
    const secciones = document.querySelectorAll('section[id]');
    const navLinks = document.querySelectorAll('.header__nav-link');
    window.addEventListener('scroll', () => {
        let actual = '';
        secciones.forEach(sec => {
            const top = sec.offsetTop - 100;
            if (window.scrollY >= top) {
                actual = sec.getAttribute('id');
            }
        });
        navLinks.forEach(link => {
            link.classList.remove('active');
            if (link.getAttribute('href') === '#' + actual) {
                link.classList.add('active');
            }
        });
    });

    // ----- CERRAR MODALES CON TECLA ESC -----
    document.addEventListener('keydown', (e) => {
        if (e.key === 'Escape') {
            cerrarTodosLosModales();
        }
    });

    // ----- ANIMACIONES DE ENTRADA CON INTERSECTION OBSERVER -----
    const observerOptions = { threshold: 0.15, rootMargin: '0px 0px -50px 0px' };
    const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                entry.target.style.opacity = '1';
                entry.target.style.transform = 'translateY(0)';
            }
        });
    }, observerOptions);

    document.querySelectorAll('.product-card, .value-card, .mv-card, .review-card, .blog-card, .contact__form').forEach(el => {
        el.style.opacity = '0';
        el.style.transform = 'translateY(30px)';
        el.style.transition = 'opacity 0.6s ease, transform 0.6s ease';
        observer.observe(el);
    });

    console.log('💪 Sudor y Gloria - Sitio web listo.');
});
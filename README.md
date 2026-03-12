<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jenzelle | CEO & Founder Portfolio</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=Montserrat:wght@300;400;600&family=Dancing+Script:wght@600&display=swap" rel="stylesheet">
    <style>
        :root {
            --coquette-pink: #fdf2f8;
            --soft-rose: #f9a8d4;
            --deep-blush: #db2777;
            --lace-pattern: url('https://www.transparenttextures.com/patterns/pinstripe.png');
        }

        body {
            font-family: 'Montserrat', sans-serif;
            background-color: var(--coquette-pink);
            color: #333;
            scroll-behavior: smooth;
        }

        .font-serif { font-family: 'Playfair Display', serif; }
        .font-cursive { font-family: 'Dancing Script', cursive; }

        .glass-nav {
            background: rgba(255, 255, 255, 0.7);
            backdrop-filter: blur(15px);
            border-bottom: 1px solid rgba(249, 168, 212, 0.3);
        }

        .hero-gradient {
            background: linear-gradient(135deg, #fdf2f8 0%, #fae8ff 100%);
        }

        .coquette-card {
            background: white;
            border-radius: 24px;
            border: 1px solid #fbcfe8;
            box-shadow: 0 15px 35px -5px rgba(219, 39, 119, 0.05);
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .coquette-card:hover {
            transform: translateY(-8px);
            border-color: var(--soft-rose);
        }

        .lace-border {
            border: 10px double #f9a8d4;
            padding: 10px;
            border-radius: 40px;
        }

        .floating {
            animation: float 4s ease-in-out infinite;
        }

        @keyframes float {
            0% { transform: translateY(0px) rotate(0deg); }
            50% { transform: translateY(-15px) rotate(2deg); }
            100% { transform: translateY(0px) rotate(0deg); }
        }

        .btn-primary {
            background: #db2777;
            color: white;
            padding: 12px 32px;
            border-radius: 50px;
            font-weight: 600;
            transition: all 0.3s;
            box-shadow: 0 4px 15px rgba(219, 39, 119, 0.3);
        }

        .btn-primary:hover {
            background: #be185d;
            transform: scale(1.05);
        }

        /* Modal Styles */
        #publishModal {
            display: none;
            position: fixed;
            inset: 0;
            background: rgba(0,0,0,0.6);
            z-index: 100;
            align-items: center;
            justify-content: center;
            backdrop-filter: blur(4px);
        }

        .modal-content {
            background: white;
            padding: 2.5rem;
            border-radius: 32px;
            max-width: 600px;
            width: 90%;
            border: 4px solid var(--soft-rose);
        }

        textarea {
            width: 100%;
            height: 150px;
            font-family: monospace;
            font-size: 10px;
            padding: 1rem;
            border-radius: 12px;
            background: #f8fafc;
            border: 1px solid #e2e8f0;
            margin-top: 1rem;
        }

        [contenteditable="true"]:focus {
            outline: 2px solid #f9a8d4;
            background: #fff;
            border-radius: 4px;
        }
    </style>
</head>
<body class="selection:bg-pink-200">

    <!-- PUBLISH MODAL -->
    <div id="publishModal">
        <div class="modal-content shadow-2xl">
            <h3 class="text-3xl font-serif text-pink-900 mb-2">Create Your Public Link</h3>
            <div class="text-sm space-y-3 text-gray-700">
                <p>1. <b>Copy</b> the code below.</p>
                <p>2. Paste it into Notepad and save as <b>index.html</b>.</p>
                <p>3. Go to <a href="https://tiiny.host" target="_blank" class="text-pink-600 underline font-bold">Tiiny.host</a> and drop your file there.</p>
                <p>4. It will give you a <b>live link</b> to send to your teacher!</p>
            </div>
            <textarea id="codeArea" readonly></textarea>
            <div class="mt-6 flex gap-4">
                <button onclick="copyCode()" class="flex-1 btn-primary">Copy Code Now</button>
                <button onclick="closePublish()" class="px-6 py-2 text-pink-600 font-semibold hover:bg-pink-50 rounded-full transition-all">Close</button>
            </div>
        </div>
    </div>

    <!-- REVISION & PUBLISH TOGGLES -->
    <div class="fixed bottom-6 right-6 z-50 flex flex-col gap-4">
        <button onclick="openPublish()" class="bg-pink-600 text-white px-6 py-4 rounded-full shadow-2xl hover:scale-105 transition-all flex items-center gap-2">
            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8.684 13.342C8.886 12.938 9 12.482 9 12c0-.482-.114-.938-.316-1.342m0 2.684a3 3 0 110-2.684m0 2.684l6.632 3.316m-6.632-6l6.632-3.316m0 0a3 3 0 105.367-2.684 3 3 0 00-5.367 2.684zm0 9.316a3 3 0 105.368 2.684 3 3 0 00-5.368-2.684z"/></svg>
            <span class="font-bold uppercase tracking-widest text-xs">Get Public Link</span>
        </button>
        <button onclick="toggleEdit()" id="editBtn" class="bg-white border-2 border-pink-200 text-pink-600 p-4 rounded-full shadow-2xl hover:scale-110 transition-all group flex items-center">
            <span id="btnText" class="hidden group-hover:inline mr-2 font-semibold text-xs uppercase tracking-widest">Edit Mode</span>
            <svg class="w-6 h-6 inline" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15.232 5.232l3.536 3.536m-2.036-5.036a2.5 2.5 0 113.536 3.536L6.5 21.036H3v-3.572L16.732 3.732z"/></svg>
        </button>
    </div>

    <!-- NAVIGATION -->
    <nav class="glass-nav fixed w-full top-0 z-40 px-8 py-5">
        <div class="max-w-7xl mx-auto flex justify-between items-center">
            <div class="text-3xl font-serif text-pink-700 font-bold italic tracking-tighter">
                Jenzelle<span class="text-pink-400 font-light">.</span>
            </div>
            <div class="hidden md:flex space-x-10 font-semibold text-xs uppercase tracking-widest text-pink-900">
                <a href="#home" class="hover:text-pink-500 transition-colors">Vision</a>
                <a href="#ict" class="hover:text-pink-500 transition-colors">ICT Role</a>
                <a href="#advocacy" class="hover:text-pink-500 transition-colors">Advocacy</a>
                <a href="#global" class="hover:text-pink-500 transition-colors">Analysis</a>
                <a href="#ethics" class="hover:text-pink-500 transition-colors">Ethics</a>
            </div>
            <a href="#contact" class="btn-primary text-xs uppercase tracking-widest px-6 py-3">Inquire</a>
        </div>
    </nav>

    <!-- SECTION 1: HOME PAGE -->
    <section id="home" class="min-h-screen pt-32 pb-20 px-6 hero-gradient relative overflow-hidden">
        <div class="absolute top-40 left-10 text-pink-200 opacity-40 floating text-8xl">✿</div>
        <div class="absolute bottom-20 right-10 text-pink-200 opacity-40 floating text-8xl" style="animation-delay: 2s">❦</div>
        
        <div class="max-w-7xl mx-auto grid lg:grid-cols-2 gap-16 items-center">
            <div class="lace-border">
                <div class="bg-white rounded-[32px] overflow-hidden shadow-2xl relative aspect-[4/5] flex items-center justify-center">
                    <img src="https://images.unsplash.com/photo-1490481651871-ab68de25d43d?q=80&w=2070&auto=format&fit=crop" class="w-full h-full object-cover opacity-90" alt="Modest High Fashion">
                    <div class="absolute inset-0 bg-pink-100/10"></div>
                </div>
            </div>
            <div class="space-y-8">
                <div class="inline-block px-4 py-1 bg-pink-200 text-pink-700 rounded-full text-xs font-bold tracking-widest uppercase mb-4" contenteditable="true">
                    Established 2026
                </div>
                <h1 class="text-6xl lg:text-8xl font-serif text-pink-900 leading-none">
                    Jenzelle <br>
                    <span class="italic font-normal text-pink-500">The CEO.</span>
                </h1>
                <p class="text-xl text-pink-800 leading-relaxed font-light italic" contenteditable="true">
                    "I am Jenzelle, the visionary Founder and CEO of my eponymous fashion house. My journey is defined by the pursuit of harmonizing deep-rooted modesty with contemporary sophistication, proving that elegance resides in what we choose to preserve."
                </p>
                <div class="p-8 bg-white/50 border border-pink-200 rounded-3xl backdrop-blur-sm">
                    <h3 class="font-serif text-2xl text-pink-900 mb-3">Professional Slogan</h3>
                    <p class="text-lg text-pink-700 italic font-cursive" contenteditable="true">
                        "Elegance in Every Layer, Integrity in Every Thread."
                    </p>
                    <p class="mt-4 text-sm text-gray-600 leading-relaxed" contenteditable="true">
                        I chose the path of a Modest Fashion Entrepreneur because of a glaring gap in the market: the need for attire that respects personal values without sacrificing the artistic expression of high fashion. Jenzelle exists to empower the modern woman with dignity.
                    </p>
                </div>
            </div>
        </div>
    </section>

    <!-- SECTION 2: ICT IN MY FUTURE PROFESSION -->
    <section id="ict" class="py-24 px-6 bg-white">
        <div class="max-w-6xl mx-auto">
            <div class="text-center mb-16">
                <h2 class="text-4xl font-serif text-pink-900">The Digital Renaissance of Fashion</h2>
                <div class="h-1 w-20 bg-pink-300 mx-auto mt-4"></div>
            </div>

            <div class="grid md:grid-cols-2 gap-12">
                <div class="coquette-card p-10">
                    <div class="text-pink-500 mb-6">
                        <svg class="w-12 h-12" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path d="M9.75 17L9 20l-1 1h8l-1-1-.75-3M3 13h18M5 17h14a2 2 0 002-2V5a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/></svg>
                    </div>
                    <h3 class="text-2xl font-serif text-pink-900 mb-4">Implementation of ICT Tools</h3>
                    <ul class="space-y-4 text-gray-600 text-sm leading-relaxed list-disc pl-5" contenteditable="true">
                        <li><strong>Computer-Aided Design (CAD):</strong> We utilize advanced 2D and 3D modeling software like CLO to simulate fabric movement, ensuring our modest cuts drape perfectly without the need for multiple physical prototypes, thereby reducing material waste.</li>
                        <li><strong>Artificial Intelligence in Forecasting:</strong> Jenzelle leverages AI-driven data analytics to predict upcoming trends in the modest fashion niche, allowing us to manage inventory efficiently and prevent overproduction.</li>
                        <li><strong>Cloud-Based Supply Chain:</strong> By using Integrated Enterprise Resource Planning (ERP) systems, I can monitor ethical textile sourcing from international suppliers in real-time, ensuring transparency from the fiber level to the finished garment.</li>
                    </ul>
                </div>
                <div class="coquette-card p-10 bg-pink-50 border-none">
                    <div class="text-pink-500 mb-6">
                        <svg class="w-12 h-12" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path d="M13 10V3L4 14h7v7l9-11h-7z"/></svg>
                    </div>
                    <h3 class="text-2xl font-serif text-pink-900 mb-4">Enhancing Professional Service</h3>
                    <p class="text-gray-600 leading-relaxed mb-6" contenteditable="true">
                        ICT serves as the bridge between my creative vision and global accessibility. Through immersive e-commerce experiences and Augmented Reality (AR) fitting rooms, Jenzelle provides customers with the confidence to purchase modest wear that fits their unique silhouettes perfectly, minimizing the need for returns and logistics-related carbon footprints.
                    </p>
                    <div class="p-6 bg-white rounded-2xl border border-pink-100">
                        <p class="text-xs font-bold text-pink-400 uppercase mb-2">Key Performance Metric</p>
                        <p class="text-pink-900 italic" contenteditable="true">"Digital integration has increased Jenzelle's operational efficiency by 40% while maintaining a 98% customer satisfaction rate through personalized digital consultations."</p>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- SECTION 3: ADVOCACY & DEVELOPMENT -->
    <section id="advocacy" class="py-24 px-6 relative overflow-hidden">
        <div class="absolute inset-0 opacity-10" style="background-image: var(--lace-pattern)"></div>
        <div class="max-w-5xl mx-auto relative z-10">
            <div class="bg-white rounded-[40px] p-12 md:p-20 shadow-xl border border-pink-100">
                <div class="text-center mb-12">
                    <span class="text-pink-500 text-sm font-bold tracking-[0.3em] uppercase">Advocacy Campaign</span>
                    <h2 class="text-5xl font-serif text-pink-900 mt-2">The Authentic Silk Project</h2>
                    <p class="text-pink-600 font-cursive text-2xl mt-2">Countering Digital Deception in Philippine Retail</p>
                </div>

                <div class="grid md:grid-cols-2 gap-12 items-start">
                    <div class="space-y-6">
                        <h4 class="text-lg font-bold text-pink-800 flex items-center gap-2">
                            <span class="w-8 h-8 rounded-full bg-pink-100 flex items-center justify-center text-xs">01</span>
                            The Problem (PH Realities)
                        </h4>
                        <p class="text-gray-600 leading-relaxed" contenteditable="true">
                            In the Philippines, the rise of "e-commerce scams" and "misleading product visuals" has severely damaged consumer trust. Many local buyers fall victim to high-budget social media ads that promise premium modest wear but deliver low-quality, synthetic imitations—often referred to as "Expectation vs. Reality" disappointments.
                        </p>
                        <h4 class="text-lg font-bold text-pink-800 flex items-center gap-2">
                            <span class="w-8 h-8 rounded-full bg-pink-100 flex items-center justify-center text-xs">02</span>
                            The ICT-Led Solution
                        </h4>
                        <p class="text-gray-600 leading-relaxed" contenteditable="true">
                            Jenzelle advocates for <strong>"Digital Fabric Transparency."</strong> We are developing a QR-code-based verification system that utilizes blockchain technology. When scanned, customers can see a live video of the fabric's tactile properties and a verified certificate of authenticity, ensuring they receive exactly what they view online.
                        </p>
                    </div>
                    <div class="bg-pink-50 rounded-3xl p-10 space-y-6 border border-pink-100">
                        <h4 class="text-xl font-serif text-pink-900">Campaign Impact</h4>
                        <div class="space-y-4">
                            <div class="flex justify-between items-end border-b border-pink-200 pb-2">
                                <span class="text-sm font-semibold text-pink-700">Digital Trust Score</span>
                                <span class="text-2xl font-serif text-pink-900">92%</span>
                            </div>
                            <div class="flex justify-between items-end border-b border-pink-200 pb-2">
                                <span class="text-sm font-semibold text-pink-700">Scam Prevention Reach</span>
                                <span class="text-2xl font-serif text-pink-900">50k+</span>
                            </div>
                        </div>
                        <p class="text-xs text-pink-400 italic" contenteditable="true">
                            "Our goal is to educate 50,000 Filipina consumers on how to identify fraudulent digital ads and protect their digital wallets from unscrupulous online vendors."
                        </p>
                        <button class="w-full btn-primary py-4">Support Our Cause</button>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- SECTION 4 & 6: CRITICAL & GLOBAL COMPARISON -->
    <section id="global" class="py-24 px-6 bg-pink-50">
        <div class="max-w-6xl mx-auto">
            <h2 class="text-4xl font-serif text-pink-900 mb-16 text-center">Global Digital Perspectives</h2>
            <div class="grid lg:grid-cols-3 gap-8">
                <!-- Influencer Opinion -->
                <div class="coquette-card p-8 bg-white">
                    <h3 class="font-serif text-xl text-pink-800 mb-4">Public Opinion & Social Media</h3>
                    <p class="text-sm text-gray-600 leading-relaxed" contenteditable="true">
                        Social media is a double-edged sword for the Jenzelle brand. While it allows us to foster a global community of modest-conscious women, the algorithm often prioritizes sensationalism over substance. One "cancel culture" misunderstanding can jeopardize years of brand building. Therefore, we treat social media as a platform for **advocacy first** and marketing second.
                    </p>
                </div>
                <!-- Global Comparison -->
                <div class="coquette-card p-8 bg-white col-span-2">
                    <h3 class="font-serif text-xl text-pink-800 mb-4">International Infrastructure Comparison</h3>
                    <div class="grid md:grid-cols-2 gap-8">
                        <div>
                            <p class="text-xs font-bold text-pink-400 mb-2">Philippine Realities</p>
                            <p class="text-sm text-gray-600" contenteditable="true">
                                Operating in the Philippines presents challenges like the "Digital Divide." High data costs and intermittent connectivity in provincial areas mean Jenzelle must optimize our website for low-bandwidth usage, ensuring accessibility for customers outside major metropolitan hubs like Manila.
                            </p>
                        </div>
                        <div class="border-l border-pink-100 pl-8">
                            <p class="text-xs font-bold text-pink-400 mb-2">Global Standards (EU/UAE)</p>
                            <p class="text-sm text-gray-600" contenteditable="true">
                                In global hubs like Dubai or London, 5G ubiquity allows competitors to use data-heavy AR mirrors and instant AI-stylists. To compete globally, Jenzelle must maintain a "Global Design, Local Delivery" mindset, ensuring our digital infrastructure is robust enough for high-speed markets while remaining inclusive of local PH limitations.
                            </p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- SECTION 5: DIGITAL CITIZENSHIP & ETHICS -->
    <section id="ethics" class="py-24 px-6 bg-white">
        <div class="max-w-4xl mx-auto text-center">
            <h2 class="text-4xl font-serif text-pink-900 mb-4">The Ethical Compass of Jenzelle</h2>
            <p class="text-pink-500 font-cursive text-xl mb-12">Navigating the digital world with integrity</p>
            
            <div class="grid md:grid-cols-3 gap-6">
                <div class="space-y-4">
                    <div class="w-16 h-16 bg-pink-100 rounded-full flex items-center justify-center mx-auto text-2xl">⚖️</div>
                    <h4 class="font-bold text-pink-800">Digital Etiquette</h4>
                    <p class="text-xs text-gray-500 leading-relaxed px-4" contenteditable="true">As CEO, I enforce a "Respect-First" policy. Jenzelle’s digital representatives are trained to handle conflict with grace, ensuring that our online presence reflects the modesty we sell.</p>
                </div>
                <div class="space-y-4">
                    <div class="w-16 h-16 bg-pink-100 rounded-full flex items-center justify-center mx-auto text-2xl">🔐</div>
                    <h4 class="font-bold text-pink-800">Cybersecurity & Privacy</h4>
                    <p class="text-xs text-gray-500 leading-relaxed px-4" contenteditable="true">We strictly comply with the Data Privacy Act of 2012. Protecting our clients' personal and payment data is a moral imperative, not just a legal requirement.</p>
                </div>
                <div class="space-y-4">
                    <div class="w-16 h-16 bg-pink-100 rounded-full flex items-center justify-center mx-auto text-2xl">🌱</div>
                    <h4 class="font-bold text-pink-800">Digital Footprint</h4>
                    <p class="text-xs text-gray-500 leading-relaxed px-4" contenteditable="true">We practice sustainable digital storage. By purging unnecessary data and optimizing assets, we reduce the carbon footprint of our web servers, aligning with our eco-conscious values.</p>
                </div>
            </div>
        </div>
    </section>

    <!-- SECTION 7: CONTACT & COMPLIANCE -->
    <footer id="contact" class="bg-pink-900 text-pink-100 py-20 px-6">
        <div class="max-w-6xl mx-auto">
            <div class="flex flex-col md:flex-row justify-between items-center border-b border-pink-800 pb-16">
                <div class="mb-8 md:mb-0">
                    <h2 class="text-5xl font-serif text-white mb-4">Jenzelle<span class="text-pink-400">.</span></h2>
                    <p class="text-pink-300 italic">"The future of modest elegance is digital."</p>
                </div>
                <div class="text-right space-y-4">
                    <p class="font-bold text-white uppercase tracking-widest text-xs">Direct Office</p>
                    <p class="text-lg" contenteditable="true">ceo@jenzelle-official.com</p>
                    <div class="flex justify-end gap-4">
                        <span class="w-10 h-10 border border-pink-700 rounded-full flex items-center justify-center hover:bg-pink-800 cursor-pointer transition-colors">in</span>
                        <span class="w-10 h-10 border border-pink-700 rounded-full flex items-center justify-center hover:bg-pink-800 cursor-pointer transition-colors">ig</span>
                    </div>
                </div>
            </div>
            
            <div class="mt-16 grid md:grid-cols-2 gap-12">
                <div class="p-8 bg-pink-950/50 rounded-3xl border border-pink-800/50">
                    <h4 class="text-sm font-bold text-pink-400 uppercase mb-4 tracking-widest">Ethical Disclaimer</h4>
                    <p class="text-xs leading-relaxed text-pink-200" contenteditable="true">
                        This digital portfolio is an academic representation of Jenzelle's professional future. All data interpretations are based on current Philippine ICT trends as of 2024. We commit to maintaining a truthful digital presence and advocate against fashion-related consumer scams.
                    </p>
                </div>
                <div class="text-xs text-pink-500 flex flex-col justify-center space-y-2">
                    <p><strong>Citations:</strong></p>
                    <p>• Philippine Data Privacy Act of 2012</p>
                    <p>• DTI Philippines E-Commerce Roadmap 2022-2025</p>
                    <p>• Global Fashion ICT Report (Statista 2023)</p>
                    <p class="mt-4 opacity-50">&copy; 2026 Jenzelle Official. All Rights Reserved.</p>
                </div>
            </div>
        </div>
    </footer>

    <script>
        function toggleEdit() {
            const elements = document.querySelectorAll('[contenteditable]');
            const btn = document.getElementById('editBtn');
            const btnText = document.getElementById('btnText');
            const isEditing = elements[0].contentEditable === "true";

            elements.forEach(el => {
                el.contentEditable = !isEditing;
            });

            if (!isEditing) {
                btnText.innerText = "Lock & Save";
                btn.classList.replace('bg-white', 'bg-green-100');
            } else {
                btnText.innerText = "Edit Mode";
                btn.classList.replace('bg-green-100', 'bg-white');
            }
        }

        function openPublish() {
            const html = document.documentElement.outerHTML;
            document.getElementById('codeArea').value = html;
            document.getElementById('publishModal').style.display = 'flex';
        }

        function closePublish() {
            document.getElementById('publishModal').style.display = 'none';
        }

        function copyCode() {
            const copyText = document.getElementById("codeArea");
            copyText.select();
            document.execCommand("copy");
            alert("Code Copied! Now save it as index.html and upload to Tiiny.host to get your link.");
        }

        document.querySelectorAll('[contenteditable]').forEach(el => el.contentEditable = "false");
    </script>
</body>
</html>


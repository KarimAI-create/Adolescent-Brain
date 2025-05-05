
<html lang="en">
<head>
    <meta name="google-adsense-account" content="ca-pub-4401807132031899">
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>The Debt We Owe to the Adolescent Brain: Interactive Lesson</title>
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <link href="https://cdn.jsdelivr.net/npm/remixicon@2.5.0/fonts/remixicon.css" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
    <style>
        :root {
            --primary: #6366f1;
            --primary-light: #818cf8;
            --secondary: #4f46e5;
            --accent: #f97316;
            --dark: #1e293b;
            --light: #f8fafc;
            --success: #22c55e;
            --error: #ef4444;
            --warning: #eab308;
        }
        html {
            scroll-behavior: smooth;
            scroll-snap-type: y mandatory;
        }
        body {
            font-family: 'Poppins', sans-serif;
            overflow-x: hidden;
            background-color: var(--light);
            color: var(--dark);
        }
        .slide {
            scroll-snap-align: start;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            padding: 2rem;
            position: relative;
            opacity: 0;
            transform: translateY(20px);
            transition: opacity 0.5s ease, transform 0.5s ease;
        }
        .slide.active {
            opacity: 1;
            transform: translateY(0);
        }
        .slide-content {
            max-width: 1200px;
            margin: 0 auto;
            width: 100%;
            z-index: 10;
            background-color: rgba(255, 255, 255, 0.9);
            padding: 2rem;
            border-radius: 1rem;
            box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.1);
        }
        .bg-image {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            object-fit: cover;
            opacity: 0.2;
            z-index: 1;
        }
        .progress-bar {
            position: fixed;
            top: 0;
            left: 0;
            height: 6px;
            background-color: var(--primary);
            width: 0%;
            z-index: 1000;
            transition: width 0.3s ease;
        }
        .nav-dots {
            position: fixed;
            right: 20px;
            top: 50%;
            transform: translateY(-50%);
            z-index: 100;
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        .nav-dot {
            width: 12px;
            height: 12px;
            border-radius: 50%;
            background-color: rgba(255, 255, 255, 0.5);
            border: 2px solid var(--primary);
            cursor: pointer;
            transition: all 0.3s ease;
        }
        .nav-dot.active {
            background-color: var(--primary);
            transform: scale(1.3);
        }
        .btn {
            padding: 0.75rem 1.5rem;
            border-radius: 0.5rem;
            font-weight: 500;
            transition: all 0.3s ease;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 0.5rem;
            cursor: pointer;
        }
        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
        }
        .btn-primary {
            background-color: var(--primary);
            color: white;
        }
        .btn-secondary {
            background-color: var(--secondary);
            color: white;
        }
        .btn-accent {
            background-color: var(--accent);
            color: white;
        }
        .quiz-option {
            padding: 1rem;
            border: 2px solid #e2e8f0;
            border-radius: 0.5rem;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-bottom: 0.5rem;
        }
        .quiz-option:hover {
            border-color: var(--primary-light);
            background-color: rgba(99, 102, 241, 0.05);
        }
        .quiz-option.selected {
            border-color: var(--primary);
            background-color: rgba(99, 102, 241, 0.1);
        }
        .quiz-option.correct {
            border-color: var(--success);
            background-color: rgba(34, 197, 94, 0.1);
        }
        .quiz-option.incorrect {
            border-color: var(--error);
            background-color: rgba(239, 68, 68, 0.1);
        }
        .feedback {
            padding: 1rem;
            border-radius: 0.5rem;
            margin-top: 1rem;
            display: none;
        }
        .feedback.success {
            background-color: rgba(34, 197, 94, 0.1);
            color: var(--success);
            border: 1px solid var(--success);
        }
        .feedback.error {
            background-color: rgba(239, 68, 68, 0.1);
            color: var(--error);
            border: 1px solid var(--error);
        }
        .audio-controls {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            margin-top: 1rem;
        }
        .audio-btn {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            background-color: var(--primary);
            color: white;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        .audio-btn:hover {
            background-color: var(--secondary);
            transform: scale(1.1);
        }
        .kahoot-question {
            background-color: white;
            padding: 2rem;
            border-radius: 1rem;
            box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.1);
            margin-bottom: 1rem;
            max-width: 800px;
            margin: 0 auto;
        }
        .kahoot-options {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 1rem;
            margin-top: 1.5rem;
        }
        .kahoot-option {
            padding: 1.5rem;
            border-radius: 0.5rem;
            cursor: pointer;
            font-weight: 600;
            text-align: center;
            color: white;
            transition: all 0.3s ease;
        }
        .kahoot-option:hover {
            transform: scale(1.03);
        }
        .kahoot-option:nth-child(1) {
            background-color: #e21b3c;
        }
        .kahoot-option:nth-child(2) {
            background-color: #1368ce;
        }
        .kahoot-option:nth-child(3) {
            background-color: #d89e00;
        }
        .kahoot-option:nth-child(4) {
            background-color: #26890c;
        }
        .kahoot-timer {
            width: 100%;
            height: 10px;
            background-color: #f0f0f0;
            border-radius: 5px;
            margin-top: 1rem;
            overflow: hidden;
        }
        .kahoot-timer-progress {
            height: 100%;
            width: 100%;
            background-color: var(--primary);
            border-radius: 5px;
            transition: width 0.1s linear;
        }
        .leaderboard {
            margin-top: 2rem;
            background-color: white;
            padding: 1.5rem;
            border-radius: 1rem;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
        }
        .leaderboard-item {
            display: flex;
            align-items: center;
            padding: 0.75rem;
            border-bottom: 1px solid #f0f0f0;
        }
        .leaderboard-rank {
            width: 30px;
            height: 30px;
            border-radius: 50%;
            background-color: var(--primary);
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-right: 1rem;
            font-weight: 600;
        }
        .story-area {
            width: 100%;
            min-height: 150px;
            border: 2px solid #e2e8f0;
            border-radius: 0.5rem;
            padding: 1rem;
            font-family: 'Poppins', sans-serif;
            resize: vertical;
            transition: border-color 0.3s ease;
        }
        .story-area:focus {
            outline: none;
            border-color: var(--primary);
        }
        @media (max-width: 768px) {
            .slide-content {
                padding: 1.5rem;
            }
            .kahoot-options {
                grid-template-columns: 1fr;
            }
            .nav-dots {
                right: 10px;
            }
        }
        .highlight {
            background-color: rgba(234, 179, 8, 0.2);
            padding: 0 0.25rem;
            border-radius: 0.25rem;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 1.5rem 0;
        }
        table th, table td {
            border: 1px solid #e2e8f0;
            padding: 0.75rem;
            text-align: left;
        }
        table th {
            background-color: #f8fafc;
            font-weight: 600;
        }
        .fade-in {
            animation: fadeIn 0.5s ease forwards;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .bounce {
            animation: bounce 1s infinite;
        }
        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }
    </style>
</head>
<body>
    <div class="progress-bar" id="progressBar"></div>
    
    <nav class="nav-dots" id="navDots"></nav>

    <!-- Introduction Slide -->
    <section id="slide1" class="slide">
        <img src="https://images.unsplash.com/photo-1503387762-592deb58ef4e?ixlib=rb-1.2.1&auto=format&fit=crop&w=1050&q=80" alt="Teenagers looking at sunset" class="bg-image">
        <div class="slide-content">
            <h1 class="text-4xl md:text-5xl font-bold mb-4 text-center text-indigo-600">The Debt We Owe to the Adolescent Brain</h1>
            <h2 class="text-xl md:text-2xl text-center text-gray-600 mb-8">Informational text by Jeanne Miller</h2>
            
            <p class="text-lg mb-6">The teenage years are a time of amazing growth and adaptation for the human brain. During this interactive lesson, we'll explore the unique features of adolescent brain development and understand why this period is crucial for human adaptability and success.</p>
            
            <div class="flex justify-center mb-4">
                <div class="audio-controls">
                    <button class="audio-btn read-aloud" aria-label="Read aloud" data-slide="slide1">
                        <i class="ri-volume-up-line"></i>
                    </button>
                    <select class="voice-select px-2 py-1 rounded border border-gray-300">
                        <option value="US English">US English</option>
                        <option value="UK English">UK English</option>
                        <option value="Australian English">Australian English</option>
                        <option value="Indian English">Indian English</option>
                    </select>
                </div>
            </div>
            
            <div class="text-center mt-10">
                <button class="btn btn-primary next-slide" data-next="slide2">Begin the Journey <i class="ri-arrow-right-line"></i></button>
            </div>
        </div>
    </section>

    <!-- Why Humans Are So Adaptable -->
    <section id="slide2" class="slide">
        <img src="https://images.unsplash.com/photo-1522202176988-66273c2fd55f?ixlib=rb-1.2.1&auto=format&fit=crop&w=1050&q=80" alt="Group of diverse teenagers" class="bg-image">
        <div class="slide-content">
            <h2 class="text-3xl font-bold mb-6 text-indigo-600">Why Humans Are So Adaptable</h2>
            
            <div class="text-lg mb-6">
                <p class="mb-4">"Polar bears can live above the Arctic Circle but they can't live at the Equator. Gorillas can live at the Equator but they can't live above the Arctic Circle. Humans, however, can live in the Arctic or they can live in the tropics. Why is our species so adaptable?"</p>
                
                <p class="mb-4">Most mammals have a brief period of adolescence. But humans, under the protection of their families, take many years to develop and grow into adulthood. This extended period allows our brains to develop exactly the skills we need for our environment.</p>
                
                <p class="mb-4">This is one key difference between humans and other species, including our evolutionary relatives like Neanderthals. Our long adolescence gives us a significant advantage in terms of adaptability.</p>
            </div>
            
            <div class="bg-indigo-50 p-4 rounded-lg mb-6">
                <h3 class="font-semibold text-indigo-700 mb-2">Key Concept</h3>
                <p>Human adaptability comes from our extended adolescence period, which allows our brains to develop in response to our specific environments.</p>
            </div>
            
            <div class="flex justify-between items-center mt-8">
                <div class="audio-controls">
                    <button class="audio-btn read-aloud" aria-label="Read aloud" data-slide="slide2">
                        <i class="ri-volume-up-line"></i>
                    </button>
                </div>
                
                <div>
                    <button class="btn btn-secondary next-slide" data-next="slide3">Next <i class="ri-arrow-right-line"></i></button>
                </div>
            </div>
        </div>
    </section>

    <!-- Brain Under Construction -->
    <section id="slide3" class="slide">
        <img src="https://images.unsplash.com/photo-1559757175-5700dde675bc?ixlib=rb-1.2.1&auto=format&fit=crop&w=1489&q=80" alt="Construction concept" class="bg-image">
        <div class="slide-content">
            <h2 class="text-3xl font-bold mb-6 text-indigo-600">Brain Under Construction</h2>
            
            <div class="text-lg mb-6">
                <p class="mb-4">Dr. Jay Giedd, professor of psychiatry at the University of California at San Diego, explains: "Nothing is even close to humans in terms of how long we're dependent on caregivers."</p>
                
                <p class="mb-4">During adolescence, our brains undergo a fascinating process:</p>
                <ul class="list-disc pl-6 mb-4 space-y-2">
                    <li>First, there's an <span class="highlight">overproduction of neural connections</span></li>
                    <li>Then, these connections <span class="highlight">"fight it out"</span> - the ones that are used stay, others are eliminated</li>
                    <li>We lose "gray matter" and gain "white matter" (myelin)</li>
                    <li>Myelin speeds up communication between nerve cells</li>
                </ul>
                
                <p class="mb-4">As Giedd puts it: <em>"You're asking your brain, 'What do I need to be good at? What do I need to do to make it in this world?' Every choice you make trains your brain."</em></p>
            </div>
            
            <div class="bg-yellow-50 p-4 rounded-lg mb-6">
                <h3 class="font-semibold text-yellow-700 mb-2">Did You Know?</h3>
                <p>Neanderthals had brains about 13% bigger than ours, but they couldn't adapt to changing environments as effectively as humans.</p>
            </div>
            
            <div class="flex justify-between items-center mt-8">
                <div class="audio-controls">
                    <button class="audio-btn read-aloud" aria-label="Read aloud" data-slide="slide3">
                        <i class="ri-volume-up-line"></i>
                    </button>
                </div>
                
                <div>
                    <button class="btn btn-secondary next-slide" data-next="slide4">Next <i class="ri-arrow-right-line"></i></button>
                </div>
            </div>
        </div>
    </section>

    <!-- Moving On from Childhood -->
    <section id="slide4" class="slide">
        <img src="https://images.unsplash.com/photo-1529333166437-7750a6dd5a70?ixlib=rb-1.2.1&auto=format&fit=crop&w=1489&q=80" alt="Teenager with parents" class="bg-image">
        <div class="slide-content">
            <h2 class="text-3xl font-bold mb-6 text-indigo-600">Moving On from Childhood</h2>
            
            <div class="text-lg mb-6">
                <p class="mb-4">Dr. B. J. Casey, a professor of psychology at Weill Cornell Medical College, has found that adolescent behaviors are consistent across species:</p>
                
                <ul class="list-disc pl-6 mb-4 space-y-2">
                    <li>Hanging out with same-aged peers</li>
                    <li>Having more conflicts with parents</li>
                    <li>Being sensitive to peer influence</li>
                    <li>Taking risks</li>
                    <li>Pulling away from parents</li>
                </ul>
                
                <p class="mb-4">These behaviors have evolutionary roots. Casey explains: <em>"If you're getting all your needs met, why in the world would you leave? There needs to be some push-pull tension in evolution to get you to leave that home. Otherwise you'll deplete all the resources and it will be difficult to find a mate to partner with."</em></p>
            </div>
            
            <div class="bg-green-50 p-4 rounded-lg mb-6">
                <h3 class="font-semibold text-green-700 mb-2">Evolutionary Perspective</h3>
                <p>From an evolutionary standpoint, adolescent behaviors help young people leave home, find mates, and establish their own lives - essential steps for species survival.</p>
            </div>
            
            <div class="flex justify-between items-center mt-8">
                <div class="audio-controls">
                    <button class="audio-btn read-aloud" aria-label="Read aloud" data-slide="slide4">
                        <i class="ri-volume-up-line"></i>
                    </button>
                </div>
                
                <div>
                    <button class="btn btn-secondary next-slide" data-next="slide5">Next <i class="ri-arrow-right-line"></i></button>
                </div>
            </div>
        </div>
    </section>

    <!-- Rewards and Risks -->
    <section id="slide5" class="slide">
        <img src="https://images.unsplash.com/photo-1531206715517-5c0ba140b2b8?ixlib=rb-1.2.1&auto=format&fit=crop&w=1050&q=80" alt="Teenager taking a risk" class="bg-image">
        <div class="slide-content">
            <h2 class="text-3xl font-bold mb-6 text-indigo-600">Rewards and Risks</h2>
            
            <div class="text-lg mb-6">
                <p class="mb-4">The adolescent brain is particularly sensitive to rewards. Research has shown that teenagers have an exaggerated response in the reward center of their brains compared to children and adults.</p>
                
                <p class="mb-4">This sensitivity to rewards can drive important behaviors:</p>
                <ul class="list-disc pl-6 mb-4 space-y-2">
                    <li>Taking calculated risks that may lead to rewards</li>
                    <li>Being highly responsive to peer approval</li>
                    <li>Finding smiling faces "almost irresistible"</li>
                </ul>
                
                <p class="mb-4">Dr. Giedd notes: <em>"High risk equals high reward at times."</em></p>
                
                <p>At the same time, this risk-taking tendency has downsides in the modern world. Teenagers face a 200% increase in the chance of dying compared to children, primarily due to accidents.</p>
            </div>
            
            <div class="mt-8">
                <h3 class="text-xl font-semibold mb-4 text-indigo-600">Brain Response to Rewards</h3>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4 text-center">
                    <div class="bg-blue-50 p-4 rounded-lg">
                        <h4 class="font-medium mb-2">Children</h4>
                        <div class="w-full bg-gray-200 rounded-full h-4 mb-2">
                            <div class="bg-blue-400 h-4 rounded-full" style="width: 30%"></div>
                        </div>
                        <p>Moderate response</p>
                    </div>
                    <div class="bg-purple-50 p-4 rounded-lg">
                        <h4 class="font-medium mb-2">Teenagers</h4>
                        <div class="w-full bg-gray-200 rounded-full h-4 mb-2">
                            <div class="bg-purple-500 h-4 rounded-full" style="width: 80%"></div>
                        </div>
                        <p>Exaggerated response</p>
                    </div>
                    <div class="bg-teal-50 p-4 rounded-lg">
                        <h4 class="font-medium mb-2">Adults</h4>
                        <div class="w-full bg-gray-200 rounded-full h-4 mb-2">
                            <div class="bg-teal-400 h-4 rounded-full" style="width: 40%"></div>
                        </div>
                        <p>Moderate response</p>
                    </div>
                </div>
            </div>
            
            <div class="flex justify-between items-center mt-8">
                <div class="audio-controls">
                    <button class="audio-btn read-aloud" aria-label="Read aloud" data-slide="slide5">
                        <i class="ri-volume-up-line"></i>
                    </button>
                </div>
                
                <div>
                    <button class="btn btn-secondary next-slide" data-next="slide6">Next <i class="ri-arrow-right-line"></i></button>
                </div>
            </div>
        </div>
    </section>

    <!-- Stone Age Impulses in the Modern World -->
    <section id="slide6" class="slide">
        <img src="https://images.unsplash.com/photo-1504384308090-c894fdcc538d?ixlib=rb-1.2.1&auto=format&fit=crop&w=1050&q=80" alt="Modern teenagers with technology" class="bg-image">
        <div class="slide-content">
            <h2 class="text-3xl font-bold mb-6 text-indigo-600">Stone Age Impulses in the Modern World</h2>
            
            <div class="text-lg mb-6">
                <p class="mb-4">Our adolescent brains evolved during very different times than today. The same impulses that helped our ancestors survive now express themselves in a modern context.</p>
                
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6 my-6">
                    <div class="bg-amber-50 p-4 rounded-lg">
                        <h3 class="font-semibold text-amber-700 mb-2">Stone Age Adolescence</h3>
                        <ul class="list-disc pl-6 space-y-1">
                            <li>Risk-taking to find food</li>
                            <li>Seeking new territory</li>
                            <li>Building social connections for survival</li>
                            <li>Physical dangers (predators)</li>
                            <li>Natural consequences of risky behavior</li>
                        </ul>
                    </div>
                    <div class="bg-blue-50 p-4 rounded-lg">
                        <h3 class="font-semibold text-blue-700 mb-2">Modern Adolescence</h3>
                        <ul class="list-disc pl-6 space-y-1">
                            <li>Risk-taking in different contexts</li>
                            <li>Social media and digital exploration</li>
                            <li>Social status through different means</li>
                            <li>Modern dangers (accidents, substance use)</li>
                            <li>Delayed consequences of risky behavior</li>
                        </ul>
                    </div>
                </div>
                
                <p class="mb-4">Dr. Casey reminds us: <em>"Adolescents are dealing with a lot, but they should remember they have greater potential for change now than at any other time. There will be many opportunities for them to change behaviors that they don't want to engage in and to become what they want to be."</em></p>
                
                <p>Dr. Giedd adds: <em>"The challenges adolescents present to their brains now will have effects for decades. We never lose it completely, but it's never going to be as good as it is when we're adolescents."</em></p>
            </div>
            
            <div class="flex justify-between items-center mt-8">
                <div class="audio-controls">
                    <button class="audio-btn read-aloud" aria-label="Read aloud" data-slide="slide6">
                        <i class="ri-volume-up-line"></i>
                    </button>
                </div>
                
                <div>
                    <button class="btn btn-secondary next-slide" data-next="slide7">Next <i class="ri-arrow-right-line"></i></button>
                </div>
            </div>
        </div>
    </section>

    <!-- Brain Development Process -->
    <section id="slide7" class="slide">
        <img src="https://images.unsplash.com/photo-1557825835-70d97c4aa567?ixlib=rb-1.2.1&auto=format&fit=crop&w=1050&q=80" alt="Brain concept" class="bg-image">
        <div class="slide-content">
            <h2 class="text-3xl font-bold mb-6 text-indigo-600">The Adolescent Brain Development Process</h2>
            
            <div class="text-lg mb-6">
                <p class="mb-6">The adolescent brain undergoes specific developmental processes that shape its future capabilities:</p>
                
                <div class="relative overflow-hidden mb-8">
                    <div class="overflow-x-auto">
                        <table class="min-w-full">
                            <thead>
                                <tr>
                                    <th>Process</th>
                                    <th>Description</th>
                                    <th>Impact</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr>
                                    <td>Neural Overproduction</td>
                                    <td>Brain produces excess neural connections</td>
                                    <td>Creates potential for diverse skills and adaptations</td>
                                </tr>
                                <tr>
                                    <td>Pruning</td>
                                    <td>Unused connections are eliminated</td>
                                    <td>Brain becomes more efficient at frequently used skills</td>
                                </tr>
                                <tr>
                                    <td>Myelination</td>
                                    <td>Nerve fibers are coated with insulating myelin</td>
                                    <td>Faster, more efficient neural communication</td>
                                </tr>
                                <tr>
                                    <td>Prefrontal Development</td>
                                    <td>Gradual maturation of decision-making areas</td>
                                    <td>Improved impulse control and planning over time</td>
                                </tr>
                                <tr>
                                    <td>Reward System Sensitivity</td>
                                    <td>Heightened response to rewards and social approval</td>
                                    <td>Motivated learning but potential risk-taking</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
                
                <div class="bg-indigo-50 p-4 rounded-lg">
                    <h3 class="font-semibold text-indigo-700 mb-2">The Adolescent Paradox</h3>
                    <p>Teenagers are physically at their peak, yet face increased mortality due to risk-taking behaviors - this paradox reflects the tension between evolutionary adaptations and modern contexts.</p>
                </div>
            </div>
            
            <div class="mt-8">
                <h3 class="text-xl font-semibold mb-4">Watch: The Teenage Brain Explained</h3>
                <div class="aspect-w-16 aspect-h-9">
                    <iframe class="rounded-lg shadow-lg" width="100%" height="315" src="https://www.youtube.com/embed/hiduiTq1ei8" title="The Teenage Brain Explained" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
                </div>
            </div>
            
            <div class="flex justify-between items-center mt-8">
                <div class="audio-controls">
                    <button class="audio-btn read-aloud" aria-label="Read aloud" data-slide="slide7">
                        <i class="ri-volume-up-line"></i>
                    </button>
                </div>
                
                <div>
                    <button class="btn btn-secondary next-slide" data-next="slide8">Next <i class="ri-arrow-right-line"></i></button>
                </div>
            </div>
        </div>
    </section>

    <!-- Common Misconceptions -->
    <section id="slide8" class="slide">
        <img src="https://images.unsplash.com/photo-1533228876829-65c94e7b5025?ixlib=rb-1.2.1&auto=format&fit=crop&w=1050&q=80" alt="Teen thinking" class="bg-image">
        <div class="slide-content">
            <h2 class="text-3xl font-bold mb-6 text-indigo-600">Common Misconceptions About Teen Behavior</h2>
            
            <div class="text-lg mb-6">
                <p class="mb-4">Many adult perceptions about teenage behavior are based on misconceptions rather than science. Let's examine some common misunderstandings:</p>
                
                <div class="space-y-4 mb-6">
                    <div class="bg-red-50 p-4 rounded-lg">
                        <h3 class="font-semibold text-red-700 mb-2">Misconception #1: "Teens are just being rebellious"</h3>
                        <p><strong>Reality:</strong> Teen behaviors are driven by brain development and evolutionary adaptations that prepare them for independence.</p>
                    </div>
                    
                    <div class="bg-red-50 p-4 rounded-lg">
                        <h3 class="font-semibold text-red-700 mb-2">Misconception #2: "Teens are poor decision-makers"</h3>
                        <p><strong>Reality:</strong> Teens can make excellent decisions, but their brains prioritize potential rewards differently than adults.</p>
                    </div>
                    
                    <div class="bg-red-50 p-4 rounded-lg">
                        <h3 class="font-semibold text-red-700 mb-2">Misconception #3: "Teens don't understand consequences"</h3>
                        <p><strong>Reality:</strong> Teens often understand risks but their developing brains weigh social rewards more heavily than potential dangers.</p>
                    </div>
                    
                    <div class="bg-red-50 p-4 rounded-lg">
                        <h3 class="font-semibold text-red-700 mb-2">Misconception #4: "Teen behavior is just hormones"</h3>
                        <p><strong>Reality:</strong> While hormones play a role, brain development and environmental factors are equally important in shaping teen behavior.</p>
                    </div>
                </div>
                
                <div class="bg-green-50 p-4 rounded-lg">
                    <h3 class="font-semibold text-green-700 mb-2">Understanding Teen Behavior</h3>
                    <p>Recognizing that teen behaviors have biological and evolutionary roots helps adults respond with empathy rather than frustration. The adolescent brain is perfectly designed for its evolutionary purpose - preparing young people for adult independence in a changing world.</p>
                </div>
            </div>
            
            <div class="flex justify-between items-center mt-8">
                <div class="audio-controls">
                    <button class="audio-btn read-aloud" aria-label="Read aloud" data-slide="slide8">
                        <i class="ri-volume-up-line"></i>
                    </button>
                </div>
                
                <div>
                    <button class="btn btn-secondary next-slide" data-next="slide9">Next <i class="ri-arrow-right-line"></i></button>
                </div>
            </div>
        </div>
    </section>

    <!-- Quiz Section -->
    <section id="slide9" class="slide">
        <img src="https://images.unsplash.com/photo-1484069560501-87d72b0c3669?ixlib=rb-1.2.1&auto=format&fit=crop&w=1050&q=80" alt="Student taking a test" class="bg-image">
        <div class="slide-content">
            <h2 class="text-3xl font-bold mb-6 text-indigo-600">Knowledge Check: Test Your Understanding</h2>
            
            <div id="quiz-container" class="text-lg mb-6">
                <div class="quiz-progress mb-4">
                    <p class="mb-2">Question <span id="current-question">1</span> of 5</p>
                    <div class="w-full bg-gray-200 rounded-full h-2.5">
                        <div id="quiz-progress-bar" class="bg-indigo-600 h-2.5 rounded-full" style="width: 20%"></div>
                    </div>
                </div>
                
                <div id="quiz-questions">
                    <!-- Question 1 -->
                    <div class="quiz-question" data-question="1">
                        <h3 class="font-semibold mb-3">According to the text, why is human adaptability linked to adolescence?</h3>
                        <div class="quiz-options">
                            <div class="quiz-option" data-correct="false">
                                <p>Because adolescents have more energy than adults</p>
                            </div>
                            <div class="quiz-option" data-correct="true">
                                <p>Because our extended adolescence allows our brains to develop in response to our environment</p>
                            </div>
                            <div class="quiz-option" data-correct="false">
                                <p>Because teenagers learn faster than young children</p>
                            </div>
                            <div class="quiz-option" data-correct="false">
                                <p>Because human hormones are more adaptable than other species</p>
                            </div>
                        </div>
                        <div class="feedback"></div>
                    </div>
                    
                    <!-- Question 2 -->
                    <div class="quiz-question hidden" data-question="2">
                        <h3 class="font-semibold mb-3">What happens to neural connections during adolescence?</h3>
                        <div class="quiz-options">
                            <div class="quiz-option" data-correct="false">
                                <p>They gradually increase until adulthood</p>
                            </div>
                            <div class="quiz-option" data-correct="false">
                                <p>They remain stable throughout adolescence</p>
                            </div>
                            <div class="quiz-option" data-correct="true">
                                <p>There's an overproduction followed by pruning of unused connections</p>
                            </div>
                            <div class="quiz-option" data-correct="false">
                                <p>They decrease steadily from childhood to adulthood</p>
                            </div>
                        </div>
                        <div class="feedback"></div>
                    </div>
                    
                    <!-- Question 3 -->
                    <div class="quiz-question hidden" data-question="3">
                        <h3 class="font-semibold mb-3">According to Dr. Casey, why do adolescents pull away from parents?</h3>
                        <div class="quiz-options">
                            <div class="quiz-option" data-correct="false">
                                <p>Because parents are often too controlling</p>
                            </div>
                            <div class="quiz-option" data-correct="true">
                                <p>Because of evolutionary pressure to leave home, find mates, and establish independence</p>
                            </div>
                            <div class="quiz-option" data-correct="false">
                                <p>Because peer relationships become more important than family</p>
                            </div>
                            <div class="quiz-option" data-correct="false">
                                <p>Because teenagers naturally dislike authority</p>
                            </div>
                        </div>
                        <div class="feedback"></div>
                    </div>
                    
                    <!-- Question 4 -->
                    <div class="quiz-question hidden" data-question="4">
                        <h3 class="font-semibold mb-3">How do teenage brains respond to rewards compared to children and adults?</h3>
                        <div class="quiz-options">
                            <div class="quiz-option" data-correct="false">
                                <p>They have a reduced response to rewards</p>
                            </div>
                            <div class="quiz-option" data-correct="false">
                                <p>They respond exactly the same as adult brains</p>
                            </div>
                            <div class="quiz-option" data-correct="false">
                                <p>They only respond to monetary rewards</p>
                            </div>
                            <div class="quiz-option" data-correct="true">
                                <p>They have an exaggerated response in the brain's reward center</p>
                            </div>
                        </div>
                        <div class="feedback"></div>
                    </div>
                    
                    <!-- Question 5 -->
                    <div class="quiz-question hidden" data-question="5">
                        <h3 class="font-semibold mb-3">What is the "adolescent paradox" mentioned in the presentation?</h3>
                        <div class="quiz-options">
                            <div class="quiz-option" data-correct="true">
                                <p>Teenagers are at their physical peak but face increased mortality due to risk-taking</p>
                            </div>
                            <div class="quiz-option" data-correct="false">
                                <p>Teenagers want independence but still need parental support</p>
                            </div>
                            <div class="quiz-option" data-correct="false">
                                <p>Teenagers learn quickly but often make poor decisions</p>
                            </div>
                            <div class="quiz-option" data-correct="false">
                                <p>Teenagers have more energy but less motivation than adults</p>
                            </div>
                        </div>
                        <div class="feedback"></div>
                    </div>
                </div>
                
                <div class="mt-6 flex justify-center">
                    <button id="check-answer" class="btn btn-primary">Check Answer</button>
                    <button id="next-question" class="btn btn-secondary ml-4 hidden">Next Question</button>
                </div>
                
                <div id="quiz-results" class="mt-8 p-6 bg-indigo-50 rounded-lg text-center hidden">
                    <h3 class="text-2xl font-bold text-indigo-600 mb-4">Quiz Results</h3>
                    <p class="text-xl mb-2">You scored: <span id="quiz-score" class="font-bold">0</span> out of 5</p>
                    <p class="mb-4" id="quiz-message"></p>
                    <button id="restart-quiz" class="btn btn-primary">Restart Quiz</button>
                    <button class="btn btn-secondary ml-4 next-slide" data-next="slide10">Continue to Next Section</button>
                </div>
            </div>
            
            <div class="flex justify-between items-center mt-8">
                <div class="audio-controls">
                    <button class="audio-btn read-aloud" aria-label="Read aloud" data-slide="slide9">
                        <i class="ri-volume-up-line"></i>
                    </button>
                </div>
            </div>
        </div>
    </section>

    <!-- Interactive Exercises -->
    <section id="slide10" class="slide">
        <img src="https://images.unsplash.com/photo-1523240795612-9a054b0db644?ixlib=rb-1.2.1&auto=format&fit=crop&w=1050&q=80" alt="Students working together" class="bg-image">
        <div class="slide-content">
            <h2 class="text-3xl font-bold mb-6 text-indigo-600">Interactive Exercise: Brain Development Case Studies</h2>
            
            <div class="text-lg mb-6">
                <p class="mb-4">Complete these adolescent scenarios by selecting the appropriate brain development principle that explains each situation.</p>
                
                <div class="exercise-container space-y-6 mb-6">
                    <!-- Exercise 1 -->
                    <div class="bg-white p-4 rounded-lg shadow-sm">
                        <h3 class="font-semibold mb-2">Scenario 1:</h3>
                        <p class="mb-3">Fifteen-year-old Jamie spent hours practicing guitar every day for three months, despite initial frustration. Now the same chord progressions that once seemed impossible feel natural and automatic.</p>
                        <p class="font-medium">This demonstrates:</p>
                        <select class="exercise-select w-full p-2 border rounded mt-2" data-correct="The myelination process strengthening neural pathways for practiced skills">
                            <option value="">Select the best explanation...</option>
                            <option value="Teenagers' natural talent for music">Teenagers' natural talent for music</option>
                            <option value="The myelination process strengthening neural pathways for practiced skills">The myelination process strengthening neural pathways for practiced skills</option>
                            <option value="The adolescent preference for artistic activities">The adolescent preference for artistic activities</option>
                            <option value="The impact of peer pressure on hobby selection">The impact of peer pressure on hobby selection</option>
                        </select>
                        <div class="exercise-feedback mt-2 hidden"></div>
                    </div>
                    
                    <!-- Exercise 2 -->
                    <div class="bg-white p-4 rounded-lg shadow-sm">
                        <h3 class="font-semibold mb-2">Scenario 2:</h3>
                        <p class="mb-3">Sixteen-year-old Alex knows driving too fast is dangerous but still speeds when friends are in the car encouraging it.</p>
                        <p class="font-medium">This demonstrates:</p>
                        <select class="exercise-select w-full p-2 border rounded mt-2" data-correct="Enhanced sensitivity to peer approval and rewards in the adolescent brain">
                            <option value="">Select the best explanation...</option>
                            <option value="Poor decision-making abilities in all teenagers">Poor decision-making abilities in all teenagers</option>
                            <option value="A lack of understanding about driving dangers">A lack of understanding about driving dangers</option>
                            <option value="Enhanced sensitivity to peer approval and rewards in the adolescent brain">Enhanced sensitivity to peer approval and rewards in the adolescent brain</option>
                            <option value="A deliberate choice to ignore safety rules">A deliberate choice to ignore safety rules</option>
                        </select>
                        <div class="exercise-feedback mt-2 hidden"></div>
                    </div>
                    
                    <!-- Exercise 3 -->
                    <div class="bg-white p-4 rounded-lg shadow-sm">
                        <h3 class="font-semibold mb-2">Scenario 3:</h3>
                        <p class="mb-3">After moving to a new country, 14-year-old Sophia quickly adapted to the language and cultural norms, while her parents struggled with the transition.</p>
                        <p class="font-medium">This demonstrates:</p>
                        <select class="exercise-select w-full p-2 border rounded mt-2" data-correct="The adolescent brain's enhanced plasticity and adaptability">
                            <option value="">Select the best explanation...</option>
                            <option value="Teenagers are naturally more intelligent than adults">Teenagers are naturally more intelligent than adults</option>
                            <option value="The adolescent brain's enhanced plasticity and adaptability">The adolescent brain's enhanced plasticity and adaptability</option>
                            <option value="Children always learn languages faster than adults">Children always learn languages faster than adults</option>
                            <option value="The parent's lack of interest in the new culture">The parent's lack of interest in the new culture</option>
                        </select>
                        <div class="exercise-feedback mt-2 hidden"></div>
                    </div>
                </div>
                
                <div class="text-center mt-8">
                    <button id="check-exercises" class="btn btn-primary">Check Answers</button>
                </div>
                
                <div id="exercise-results" class="mt-8 p-6 bg-indigo-50 rounded-lg text-center hidden">
                    <h3 class="text-2xl font-bold text-indigo-600 mb-4">Exercise Results</h3>
                    <p class="text-xl mb-2">You scored: <span id="exercise-score" class="font-bold">0</span> out of 3</p>
                    <p class="mb-4" id="exercise-message"></p>
                    <button id="restart-exercises" class="btn btn-primary">Try Again</button>
                    <button class="btn btn-secondary ml-4 next-slide" data-next="slide11">Continue to Kahoot Game</button>
                </div>
            </div>
            
            <div class="flex justify-between items-center mt-8">
                <div class="audio-controls">
                    <button class="audio-btn read-aloud" aria-label="Read aloud" data-slide="slide10">
                        <i class="ri-volume-up-line"></i>
                    </button>
                </div>
            </div>
        </div>
    </section>

    <!-- Kahoot-like Game -->
    <section id="slide11" class="slide">
        <img src="https://images.unsplash.com/photo-1516187594981-c1777cd3e6be?ixlib=rb-1.2.1&auto=format&fit=crop&w=1050&q=80" alt="Colorful game background" class="bg-image">
        <div class="slide-content">
            <h2 class="text-3xl font-bold mb-6 text-indigo-600">Brain Challenge Game</h2>
            
            <div id="kahoot-intro" class="text-center">
                <p class="text-lg mb-6">Test your knowledge about the adolescent brain with this fast-paced game! Answer quickly for more points.</p>
                <button id="start-kahoot" class="btn btn-accent text-xl py-4 px-8 bounce">Start Game!</button>
            </div>
            
            <div id="kahoot-game" class="hidden">
                <div class="kahoot-header flex justify-between items-center mb-4">
                    <div class="kahoot-question-number text-lg font-semibold">Question <span id="current-kahoot-question">1</span>/10</div>
                    <div class="kahoot-score text-lg font-semibold">Score: <span id="kahoot-score">0</span></div>
                </div>
                
                <div class="kahoot-question mb-4">
                    <h3 id="kahoot-question-text" class="text-xl font-bold mb-3">Question text goes here</h3>
                    <div class="kahoot-timer">
                        <div id="kahoot-timer-progress" class="kahoot-timer-progress"></div>
                    </div>
                </div>
                
                <div class="kahoot-options">
                    <div class="kahoot-option" data-index="0"></div>
                    <div class="kahoot-option" data-index="1"></div>
                    <div class="kahoot-option" data-index="2"></div>
                    <div class="kahoot-option" data-index="3"></div>
                </div>
                
                <div id="kahoot-feedback" class="mt-6 p-4 rounded-lg text-center hidden"></div>
            </div>
            
            <div id="kahoot-results" class="hidden text-center">
                <h3 class="text-2xl font-bold text-indigo-600 mb-4">Game Complete!</h3>
                <p class="text-xl mb-4">Your final score: <span id="final-kahoot-score" class="font-bold">0</span></p>
                
                <div class="leaderboard mb-6">
                    <h4 class="text-lg font-semibold mb-2">Top Scores</h4>
                    <div id="kahoot-leaderboard" class="bg-white rounded-lg p-4">
                        <div class="leaderboard-item">
                            <div class="leaderboard-rank">1</div>
                            <div class="flex-1">Your Score</div>
                            <div class="font-bold" id="leaderboard-score">0</div>
                        </div>
                        <div class="leaderboard-item">
                            <div class="leaderboard-rank">2</div>
                            <div class="flex-1">Average Player</div>
                            <div class="font-bold">750</div>
                        </div>
                        <div class="leaderboard-item">
                            <div class="leaderboard-rank">3</div>
                            <div class="flex-1">Beginner</div>
                            <div class="font-bold">500</div>
                        </div>
                    </div>
                </div>
                
                <button id="restart-kahoot" class="btn btn-primary">Play Again</button>
                <button class="btn btn-secondary ml-4 next-slide" data-next="slide12">Continue to Final Challenge</button>
            </div>
            
            <div class="flex justify-between items-center mt-8">
                <div class="audio-controls">
                    <button class="audio-btn read-aloud" aria-label="Read aloud" data-slide="slide11">
                        <i class="ri-volume-up-line"></i>
                    </button>
                </div>
            </div>
        </div>
    </section>

    <!-- Final Story Challenge -->
    <section id="slide12" class="slide">
        <img src="https://images.unsplash.com/photo-1532774604428-50c37203d5b5?ixlib=rb-1.2.1&auto=format&fit=crop&w=1050&q=80" alt="Creative writing" class="bg-image">
        <div class="slide-content">
            <h2 class="text-3xl font-bold mb-6 text-indigo-600">Final Story Challenge: The Adapting Brain</h2>
            
            <div class="text-lg mb-6">
                <p class="mb-4">Apply what you've learned about the adolescent brain by creating a short story that demonstrates these principles. Follow the prompts to create your narrative:</p>
                
                <div class="bg-white p-6 rounded-lg shadow-sm mb-6">
                    <h3 class="font-semibold mb-3">Story Challenge Guidelines:</h3>
                    <p class="mb-4">Create a story about a teen named Jordan who faces a significant challenge that requires adapting to a new environment or situation. Your story should include:</p>
                    <ul class="list-disc pl-6 mb-4 space-y-2">
                        <li>How Jordan's adolescent brain responds to the challenge</li>
                        <li>A risk Jordan takes that has potential rewards</li>
                        <li>The influence of peers on Jordan's decisions</li>
                        <li>How Jordan's brain adapts or "rewires" during the experience</li>
                        <li>A positive outcome that demonstrates human adaptability</li>
                    </ul>
                    
                    <textarea id="story-area" class="story-area" placeholder="Write your story here..."></textarea>
                    
                    <div class="mt-4 text-right">
                        <button id="save-story" class="btn btn-primary">Save Story</button>
                    </div>
                </div>
                
                <div id="story-feedback" class="p-4 bg-green-50 rounded-lg hidden">
                    <h3 class="font-semibold text-green-700 mb-2">Great storytelling!</h3>
                    <p>Your story demonstrates a strong understanding of adolescent brain development principles. You've successfully applied the concepts from this lesson in a creative way!</p>
                </div>
                
                <div class="bg-yellow-50 p-4 rounded-lg">
                    <h3 class="font-semibold text-yellow-700 mb-2">Story Prompts (if needed):</h3>
                    <ul class="list-disc pl-6 space-y-1">
                        <li>Jordan could be moving to a new school, learning a challenging skill, or facing a social challenge.</li>
                        <li>Consider how the adolescent brain's sensitivity to rewards might influence Jordan's choices.</li>
                        <li>Think about how the brain's "use it or lose it" principle might apply to Jordan's situation.</li>
                        <li>Remember that risk-taking isn't always negative - it can lead to growth and new opportunities.</li>
                    </ul>
                </div>
            </div>
            
            <div class="flex justify-between items-center mt-8">
                <div class="audio-controls">
                    <button class="audio-btn read-aloud" aria-label="Read aloud" data-slide="slide12">
                        <i class="ri-volume-up-line"></i>
                    </button>
                </div>
                
                <div>
                    <button class="btn btn-secondary next-slide" data-next="slide13">Next <i class="ri-arrow-right-line"></i></button>
                </div>
            </div>
        </div>
    </section>

    <!-- Conclusion -->
    <section id="slide13" class="slide">
        <img src="https://images.unsplash.com/photo-1454923634634-bd1614719a7b?ixlib=rb-1.2.1&auto=format&fit=crop&w=1050&q=80" alt="Diverse group of teenagers" class="bg-image">
        <div class="slide-content">
            <h2 class="text-3xl font-bold mb-6 text-indigo-600">Conclusion: The Debt We Owe</h2>
            
            <div class="text-lg mb-6">
                <p class="mb-4">Throughout this lesson, we've explored the remarkable adaptability of the adolescent brain and its significance for human development:</p>
                
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
                    <div class="bg-indigo-50 p-4 rounded-lg">
                        <h3 class="font-semibold text-indigo-700 mb-2">Key Takeaways</h3>
                        <ul class="list-disc pl-6 space-y-1">
                            <li>Human adaptability stems from our extended adolescence</li>
                            <li>The adolescent brain's "overproduction then pruning" creates specialized neural networks</li>
                            <li>Risk-taking and peer influence have evolutionary purposes</li>
                            <li>Modern contexts present both opportunities and dangers for adolescent development</li>
                            <li>The adolescent brain balances plasticity with increasing efficiency</li>
                        </ul>
                    </div>
                    
                    <div class="bg-purple-50 p-4 rounded-lg">
                        <h3 class="font-semibold text-purple-700 mb-2">The Bigger Picture</h3>
                        <p>As Dr. Giedd reminds us: <em>"The challenges adolescents present to their brains now will have effects for decades... it's never going to be as good as it is when we're adolescents."</em></p>
                        <p class="mt-2">This period of neuroplasticity allows humans to develop the exact skills needed for their environment - creating artists, scientists, leaders, and innovators perfectly suited to their time and place.</p>
                    </div>
                </div>
                
                <div class="bg-green-50 p-4 rounded-lg mb-6">
                    <h3 class="font-semibold text-green-700 mb-2">Essential Question</h3>
                    <p class="text-xl italic">How do the challenges you face today help to shape your future?</p>
                    <p class="mt-2">The science of adolescent brain development suggests that the challenges you navigate today are literally shaping your brain for your future. Each experience, decision, and skill you pursue is building neural pathways that will serve you throughout life.</p>
                </div>
                
                <p>Adolescence isn't merely a transition period to be endured - it's a remarkable window of opportunity that has shaped our species' success. The debt we owe to the adolescent brain is nothing less than our uniquely human adaptability and resilience.</p>
            </div>
            
            <div class="flex justify-between items-center mt-8">
                <div class="audio-controls">
                    <button class="audio-btn read-aloud" aria-label="Read aloud" data-slide="slide13">
                        <i class="ri-volume-up-line"></i>
                    </button>
                </div>
                
                <div>
                    <button class="btn btn-secondary next-slide" data-next="slide14">Next <i class="ri-arrow-right-line"></i></button>
                </div>
            </div>
        </div>
    </section>

    <!-- Additional Resources -->
    <section id="slide14" class="slide">
        <img src="https://images.unsplash.com/photo-1604872441399-ff4385fcc296?ixlib=rb-1.2.1&auto=format&fit=crop&w=1050&q=80" alt="Books and resources" class="bg-image">
        <div class="slide-content">
            <h2 class="text-3xl font-bold mb-6 text-indigo-600">Additional Resources</h2>
            
            <div class="text-lg mb-6">
                <p class="mb-6">Explore these additional resources to deepen your understanding of adolescent brain development:</p>
                
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
                    <div class="bg-white p-4 rounded-lg shadow-sm">
                        <h3 class="font-semibold text-indigo-700 mb-2">Videos</h3>
                        <ul class="space-y-3">
                            <li class="flex items-start">
                                <i class="ri-youtube-line text-red-500 mr-2 mt-1"></i>
                                <div>
                                    <a href="https://www.youtube.com/watch?v=P629TojpvDU" target="_blank" class="text-blue-600 hover:underline">Dan Siegel: The Adolescent Brain</a>
                                    <p class="text-sm text-gray-600">Dr. Dan Siegel explains the changes happening in the adolescent brain.</p>
                                </div>
                            </li>
                            <li class="flex items-start">
                                <i class="ri-youtube-line text-red-500 mr-2 mt-1"></i>
                                <div>
                                    <a href="https://www.youtube.com/watch?v=FN6ZC3g2Yxs" target="_blank" class="text-blue-600 hover:underline">TED: The Mysterious Workings of the Adolescent Brain</a>
                                    <p class="text-sm text-gray-600">Sarah-Jayne Blakemore's popular TED talk on adolescent neuroscience.</p>
                                </div>
                            </li>
                            <li class="flex items-start">
                                <i class="ri-youtube-line text-red-500 mr-2 mt-1"></i>
                                <div>
                                    <a href="https://www.youtube.com/watch?v=0O1u5OEc5eY" target="_blank" class="text-blue-600 hover:underline">Crash Course: Development of the Adolescent Brain</a>
                                    <p class="text-sm text-gray-600">Fast-paced overview of adolescent brain development.</p>
                                </div>
                            </li>
                        </ul>
                    </div>
                    
                    <div class="bg-white p-4 rounded-lg shadow-sm">
                        <h3 class="font-semibold text-indigo-700 mb-2">Articles & Books</h3>
                        <ul class="space-y-3">
                            <li class="flex items-start">
                                <i class="ri-article-line text-amber-500 mr-2 mt-1"></i>
                                <div>
                                    <a href="https://www.nimh.nih.gov/health/publications/the-teen-brain-7-things-to-know" target="_blank" class="text-blue-600 hover:underline">The Teen Brain: 7 Things to Know (NIMH)</a>
                                    <p class="text-sm text-gray-600">Essential facts about adolescent brain development from the National Institute of Mental Health.</p>
                                </div>
                            </li>
                            <li class="flex items-start">
                                <i class="ri-book-open-line text-teal-500 mr-2 mt-1"></i>
                                <div>
                                    <p class="font-medium">Brainstorm: The Power and Purpose of the Teenage Brain</p>
                                    <p class="text-sm text-gray-600">By Dr. Daniel Siegel - A comprehensive guide to understanding the adolescent brain.</p>
                                </div>
                            </li>
                            <li class="flex items-start">
                                <i class="ri-book-open-line text-teal-500 mr-2 mt-1"></i>
                                <div>
                                    <p class="font-medium">The Teenage Brain: A Neuroscientist's Survival Guide</p>
                                    <p class="text-sm text-gray-600">By Dr. Frances E. Jensen - Research-based insights into adolescent brain development.</p>
                                </div>
                            </li>
                        </ul>
                    </div>
                </div>
                
                <div class="bg-white p-4 rounded-lg shadow-sm mb-6">
                    <h3 class="font-semibold text-indigo-700 mb-2">Interactive Tools & Activities</h3>
                    <ul class="space-y-3">
                        <li class="flex items-start">
                            <i class="ri-brain-line text-purple-500 mr-2 mt-1"></i>
                            <div>
                                <a href="https://www.brainfacts.org/3d-brain" target="_blank" class="text-blue-600 hover:underline">Interactive 3D Brain</a>
                                <p class="text-sm text-gray-600">Explore brain regions and their functions with this interactive tool.</p>
                            </div>
                        </li>
                        <li class="flex items-start">
                            <i class="ri-game-line text-green-500 mr-2 mt-1"></i>
                            <div>
                                <a href="https://www.pbs.org/wgbh/pages/frontline/shows/teenbrain/view/" target="_blank" class="text-blue-600 hover:underline">PBS Frontline: Inside the Teenage Brain</a>
                                <p class="text-sm text-gray-600">Documentary and interactive features about adolescent development.</p>
                            </div>
                        </li>
                    </ul>
                </div>
                
                <div class="text-center">
                    <p class="italic">Remember: "The challenges adolescents present to their brains now will have effects for decades."</p>
                </div>
            </div>
            
            <div class="flex justify-between items-center mt-8">
                <div class="audio-controls">
                    <button class="audio-btn read-aloud" aria-label="Read aloud" data-slide="slide14">
                        <i class="ri-volume-up-line"></i>
                    </button>
                </div>
                
                <div>
                    <button class="btn btn-secondary next-slide" data-next="slide15">Next <i class="ri-arrow-right-line"></i></button>
                </div>
            </div>
        </div>
    </section>

    <!-- Credits & Acknowledgements -->
    <section id="slide15" class="slide">
        <img src="https://images.unsplash.com/photo-1434030216411-0b793f4b4173?ixlib=rb-1.2.1&auto=format&fit=crop&w=1050&q=80" alt="Thank you concept" class="bg-image">
        <div class="slide-content">
            <h2 class="text-3xl font-bold mb-6 text-center text-indigo-600">Credits & Acknowledgements</h2>
            
            <div class="text-lg mb-6 text-center">
                <p class="mb-6">Thank you for participating in this interactive lesson on adolescent brain development!</p>
                
                <div class="space-y-4 mb-6">
                    <div>
                        <h3 class="font-semibold">Original Text</h3>
                        <p>"The Debt We Owe to the Adolescent Brain" by Jeanne Miller</p>
                    </div>
                    
                    <div>
                        <h3 class="font-semibold">Images</h3>
                        <p>All background images courtesy of Unsplash photographers</p>
                    </div>
                    
                    <div>
                        <h3 class="font-semibold">Referenced Experts</h3>
                        <p>Dr. Jay Giedd, University of California at San Diego</p>
                        <p>Dr. B. J. Casey, Weill Cornell Medical College</p>
                    </div>
                </div>
                
                <div class="bg-indigo-50 p-6 rounded-lg inline-block">
                    <h3 class="font-semibold text-indigo-700 mb-2">Your Progress</h3>
                    <p>Slides completed: <span id="total-slides-completed">15/15</span></p>
                    <p>Quiz score: <span id="final-quiz-score">Pending</span></p>
                    <p>Exercise score: <span id="final-exercise-score">Pending</span></p>
                    <p>Game score: <span id="final-game-score">Pending</span></p>
                </div>
                
                <div class="mt-8">
                    <button id="restart-presentation" class="btn btn-primary">Restart Presentation</button>
                </div>
            </div>
        </div>
    </section>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // Initialize variables
            let currentSlide = 1;
            const totalSlides = document.querySelectorAll('.slide').length;
            let quizScore = 0;
            let exerciseScore = 0;
            let kahootScore = 0;
            let speechSynthesis = window.speechSynthesis;
            let utterance;
            let currentVoiceIndex = 0;
            let voices = [];
            
            // Slide navigation functions
            function updateProgressBar() {
                const progress = (currentSlide / totalSlides) * 100;
                document.getElementById('progressBar').style.width = `${progress}%`;
            }
            
            function showSlide(slideNumber) {
                // Hide all slides
                document.querySelectorAll('.slide').forEach(slide => {
                    slide.classList.remove('active');
                });
                
                // Show the selected slide
                const slideToShow = document.getElementById(`slide${slideNumber}`);
                slideToShow.classList.add('active');
                
                // Update progress bar
                currentSlide = slideNumber;
                updateProgressBar();
                
                // Update navigation dots
                updateNavDots();
                
                // Store current slide in localStorage
                localStorage.setItem('currentSlide', slideNumber);
                
                // Stop any ongoing speech
                if (speechSynthesis && utterance) {
                    speechSynthesis.cancel();
                }
            }
            
            function createNavDots() {
                const navDotsContainer = document.getElementById('navDots');
                
                for (let i = 1; i <= totalSlides; i++) {
                    const dot = document.createElement('div');
                    dot.className = 'nav-dot';
                    dot.setAttribute('data-slide', i);
                    dot.setAttribute('aria-label', `Go to slide ${i}`);
                    dot.setAttribute('tabindex', '0');
                    dot.addEventListener('click', () => showSlide(i));
                    dot.addEventListener('keydown', (e) => {
                        if (e.key === 'Enter' || e.key === ' ') {
                            showSlide(i);
                        }
                    });
                    navDotsContainer.appendChild(dot);
                }
            }
            
            function updateNavDots() {
                const dots = document.querySelectorAll('.nav-dot');
                dots.forEach((dot, index) => {
                    if (index + 1 === currentSlide) {
                        dot.classList.add('active');
                    } else {
                        dot.classList.remove('active');
                    }
                });
            }
            
            // Next slide buttons
            document.querySelectorAll('.next-slide').forEach(button => {
                button.addEventListener('click', function() {
                    const nextSlide = parseInt(this.getAttribute('data-next'));
                    showSlide(nextSlide);
                });
            });
            
            // Initialize slide navigation dots
            createNavDots();
            
            // Initialize the presentation
            function initializePresentation() {
                // Check if there's a stored slide
                const storedSlide = localStorage.getItem('currentSlide');
                if (storedSlide) {
                    showSlide(parseInt(storedSlide));
                } else {
                    showSlide(1);
                }
                
                // Initialize observers for slide animations
                const slideObserver = new IntersectionObserver((entries) => {
                    entries.forEach(entry => {
                        if (entry.isIntersecting) {
                            entry.target.classList.add('active');
                        } else {
                            entry.target.classList.remove('active');
                        }
                    });
                }, { threshold: 0.1 });
                
                document.querySelectorAll('.slide').forEach(slide => {
                    slideObserver.observe(slide);
                });
            }
            
            // Text-to-Speech functionality
            function loadVoices() {
                voices = speechSynthesis.getVoices();
            }
            
            if (speechSynthesis) {
                loadVoices();
                speechSynthesis.onvoiceschanged = loadVoices;
            }
            
            function getVoice(accentName) {
                const accentMap = {
                    'US English': 'en-US',
                    'UK English': 'en-GB',
                    'Australian English': 'en-AU',
                    'Indian English': 'en-IN'
                };
                
                const code = accentMap[accentName];
                return voices.find(voice => voice.lang.includes(code)) || voices.find(voice => voice.lang.includes('en')) || voices[0];
            }
            
            document.querySelectorAll('.read-aloud').forEach(button => {
                button.addEventListener('click', function() {
                    if (speechSynthesis) {
                        // Cancel any ongoing speech
                        speechSynthesis.cancel();
                        
                        // Get the slide content
                        const slideId = this.getAttribute('data-slide');
                        const slideContent = document.getElementById(slideId);
                        const textToRead = slideContent.querySelector('h2').textContent + '. ' + 
                                          Array.from(slideContent.querySelectorAll('p')).map(p => p.textContent).join('. ');
                        
                        // Create utterance
                        utterance = new SpeechSynthesisUtterance(textToRead);
                        
                        // Set voice based on selection
                        const accentName = document.querySelector('.voice-select').value;
                        utterance.voice = getVoice(accentName);
                        
                        // Read the text
                        speechSynthesis.speak(utterance);
                        
                        // Update button appearance
                        this.innerHTML = '<i class="ri-stop-line"></i>';
                        
                        // Reset button when done
                        utterance.onend = () => {
                            this.innerHTML = '<i class="ri-volume-up-line"></i>';
                        };
                    }
                });
            });
            
            document.querySelectorAll('.voice-select').forEach(select => {
                select.addEventListener('change', function() {
                    if (speechSynthesis && utterance) {
                        const accentName = this.value;
                        utterance.voice = getVoice(accentName);
                        
                        // Restart speech with new voice
                        speechSynthesis.cancel();
                        speechSynthesis.speak(utterance);
                    }
                });
            });
            
            // Quiz functionality
            const quizQuestions = document.querySelectorAll('.quiz-question');
            let currentQuestionIndex = 0;
            
            document.getElementById('check-answer').addEventListener('click', function() {
                const currentQuestion = quizQuestions[currentQuestionIndex];
                const selectedOption = currentQuestion.querySelector('.quiz-option.selected');
                const feedback = currentQuestion.querySelector('.feedback');
                
                if (!selectedOption) {
                    feedback.textContent = "Please select an answer first.";
                    feedback.className = "feedback error";
                    feedback.style.display = "block";
                    return;
                }
                
                const isCorrect = selectedOption.getAttribute('data-correct') === 'true';
                
                if (isCorrect) {
                    selectedOption.classList.add('correct');
                    feedback.textContent = "Correct! Great job!";
                    feedback.className = "feedback success";
                    quizScore++;
                    
                    // Trigger confetti for correct answer
                    confetti({
                        particleCount: 100,
                        spread: 70,
                        origin: { y: 0.6 }
                    });
                } else {
                    selectedOption.classList.add('incorrect');
                    
                    // Find and highlight the correct answer
                    const correctOption = currentQuestion.querySelector('.quiz-option[data-correct="true"]');
                    correctOption.classList.add('correct');
                    
                    feedback.textContent = "Incorrect. The correct answer is highlighted.";
                    feedback.className = "feedback error";
                }
                
                feedback.style.display = "block";
                this.style.display = "none";
                document.getElementById('next-question').style.display = "inline-flex";
            });
            
            document.getElementById('next-question').addEventListener('click', function() {
                // Hide current question
                quizQuestions[currentQuestionIndex].classList.add('hidden');
                
                // Move to next question or show results
                currentQuestionIndex++;
                if (currentQuestionIndex < quizQuestions.length) {
                    // Show next question
                    quizQuestions[currentQuestionIndex].classList.remove('hidden');
                    
                    // Update progress
                    document.getElementById('current-question').textContent = currentQuestionIndex + 1;
                    document.getElementById('quiz-progress-bar').style.width = `${((currentQuestionIndex + 1) / quizQuestions.length) * 100}%`;
                    
                    // Reset buttons
                    this.style.display = "none";
                    document.getElementById('check-answer').style.display = "inline-flex";
                } else {
                    // Show quiz results
                    document.getElementById('quiz-score').textContent = quizScore;
                    document.getElementById('quiz-results').classList.remove('hidden');
                    
                    // Store score
                    localStorage.setItem('quizScore', quizScore);
                    document.getElementById('final-quiz-score').textContent = `${quizScore}/5`;
                    
                    // Display appropriate message
                    const quizMessage = document.getElementById('quiz-message');
                    if (quizScore === 5) {
                        quizMessage.textContent = "Perfect score! You've mastered the material!";
                        confetti({
                            particleCount: 200,
                            spread: 100,
                            origin: { y: 0.6 }
                        });
                    } else if (quizScore >= 3) {
                        quizMessage.textContent = "Good job! You have a solid understanding of the adolescent brain.";
                    } else {
                        quizMessage.textContent = "You might want to review the material again to strengthen your understanding.";
                    }
                }
            });
            
            // Select quiz option
            document.querySelectorAll('.quiz-option').forEach(option => {
                option.addEventListener('click', function() {
                    // Only allow selection if the answer hasn't been checked yet
                    if (!this.classList.contains('correct') && !this.classList.contains('incorrect')) {
                        // Remove selected class from all options in this question
                        const questionContainer = this.closest('.quiz-question');
                        questionContainer.querySelectorAll('.quiz-option').forEach(opt => {
                            opt.classList.remove('selected');
                        });
                        
                        // Add selected class to this option
                        this.classList.add('selected');
                    }
                });
            });
            
            document.getElementById('restart-quiz').addEventListener('click', function() {
                // Reset quiz state
                currentQuestionIndex = 0;
                quizScore = 0;
                
                // Hide all questions and show first question
                quizQuestions.forEach((question, index) => {
                    if (index === 0) {
                        question.classList.remove('hidden');
                    } else {
                        question.classList.add('hidden');
                    }
                    
                    // Reset options
                    question.querySelectorAll('.quiz-option').forEach(option => {
                        option.classList.remove('selected', 'correct', 'incorrect');
                    });
                    
                    // Reset feedback
                    const feedback = question.querySelector('.feedback');
                    feedback.style.display = "none";
                    feedback.className = "feedback";
                });
                
                // Reset progress
                document.getElementById('current-question').textContent = 1;
                document.getElementById('quiz-progress-bar').style.width = "20%";
                
                // Reset buttons
                document.getElementById('check-answer').style.display = "inline-flex";
                document.getElementById('next-question').style.display = "none";
                document.getElementById('quiz-results').classList.add('hidden');
            });
            
            // Exercise functionality
            document.getElementById('check-exercises').addEventListener('click', function() {
                const exerciseSelects = document.querySelectorAll('.exercise-select');
                exerciseScore = 0;
                
                exerciseSelects.forEach(select => {
                    const selectedValue = select.value;
                    const correctValue = select.getAttribute('data-correct');
                    const feedbackElement = select.nextElementSibling;
                    
                    if (selectedValue === correctValue) {
                        select.classList.add('border-green-500');
                        feedbackElement.classList.remove('hidden');
                        feedbackElement.classList.add('text-green-600');
                        feedbackElement.textContent = "Correct! Great analysis!";
                        exerciseScore++;
                    } else if (selectedValue) {
                        select.classList.add('border-red-500');
                        feedbackElement.classList.remove('hidden');
                        feedbackElement.classList.add('text-red-600');
                        feedbackElement.textContent = `Incorrect. The correct answer is: "${correctValue}"`;
                    } else {
                        feedbackElement.classList.remove('hidden');
                        feedbackElement.classList.add('text-amber-600');
                        feedbackElement.textContent = "Please select an answer.";
                    }
                });
                
                if (exerciseSelects.length > 0 && Array.from(exerciseSelects).every(select => select.value)) {
                    // Show exercise results
                    document.getElementById('exercise-score').textContent = exerciseScore;
                    document.getElementById('exercise-results').classList.remove('hidden');
                    
                    // Store score
                    localStorage.setItem('exerciseScore', exerciseScore);
                    document.getElementById('final-exercise-score').textContent = `${exerciseScore}/3`;
                    
                    // Display appropriate message
                    const exerciseMessage = document.getElementById('exercise-message');
                    if (exerciseScore === 3) {
                        exerciseMessage.textContent = "Perfect! You've applied the concepts excellently!";
                        confetti({
                            particleCount: 150,
                            spread: 80,
                            origin: { y: 0.6 }
                        });
                    } else if (exerciseScore >= 1) {
                        exerciseMessage.textContent = "Good effort! You're starting to connect the concepts to real situations.";
                    } else {
                        exerciseMessage.textContent = "Review the material and try again to strengthen your understanding.";
                    }
                }
            });
            
            document.getElementById('restart-exercises').addEventListener('click', function() {
                // Reset exercise state
                const exerciseSelects = document.querySelectorAll('.exercise-select');
                
                exerciseSelects.forEach(select => {
                    select.value = "";
                    select.classList.remove('border-green-500', 'border-red-500');
                    
                    const feedbackElement = select.nextElementSibling;
                    feedbackElement.classList.add('hidden');
                    feedbackElement.classList.remove('text-green-600', 'text-red-600', 'text-amber-600');
                    feedbackElement.textContent = "";
                });
                
                // Hide results
                document.getElementById('exercise-results').classList.add('hidden');
            });
            
            // Kahoot-like game functionality
            const kahootQuestions = [
                {
                    question: "Which species had brains about 13% larger than modern humans?",
                    options: ["Homo erectus", "Neanderthals", "Homo habilis", "Australopithecus"],
                    correctIndex: 1
                },
                {
                    question: "What happens to 'gray matter' during adolescent brain development?",
                    options: ["It increases steadily", "It decreases as myelin increases", "It remains constant", "It fluctuates randomly"],
                    correctIndex: 1
                },
                {
                    question: "According to Dr. Casey, what do adolescents find 'almost irresistible'?",
                    options: ["Smiling faces", "Exciting activities", "Sweet foods", "New technology"],
                    correctIndex: 0
                },
                {
                    question: "What percentage increase in mortality do teenagers face compared to children?",
                    options: ["50%", "100%", "150%", "200%"],
                    correctIndex: 3
                },
                {
                    question: "What is the main cause of adolescent mortality mentioned in the text?",
                    options: ["Disease", "Accidents", "Violence", "Substance abuse"],
                    correctIndex: 1
                },
                {
                    question: "What process strengthens frequently used neural pathways in the adolescent brain?",
                    options: ["Neurogenesis", "Synaptic pruning", "Myelination", "Cortical folding"],
                    correctIndex: 2
                },
                {
                    question: "Dr. Giedd compares adolescent brain development to what process?",
                    options: ["Building a house", "Growing a garden", "Training for a marathon", "Overproduction then pruning"],
                    correctIndex: 3
                },
                {
                    question: "What evolutionary purpose does peer influence serve for adolescents?",
                    options: ["To develop creativity", "To encourage leaving home", "To promote learning", "To improve memory"],
                    correctIndex: 1
                },
                {
                    question: "Which of these is NOT mentioned as a typical adolescent behavior?",
                    options: ["Taking risks", "Hanging out with peers", "Having conflicts with parents", "Preferring solitary activities"],
                    correctIndex: 3
                },
                {
                    question: "According to Dr. Giedd, when will the brain's adaptability be at its peak?",
                    options: ["During early childhood", "During adolescence", "During early adulthood", "During middle age"],
                    correctIndex: 1
                }
            ];
            
            let currentKahootQuestion = 0;
            let kahootTimer;
            let kahootTimeLeft = 0;
            const QUESTION_TIME = 20; // seconds
            
            // Start the Kahoot game
            document.getElementById('start-kahoot').addEventListener('click', function() {
                document.getElementById('kahoot-intro').classList.add('hidden');
                document.getElementById('kahoot-game').classList.remove('hidden');
                
                // Start the first question
                showKahootQuestion(0);
            });
            
            function showKahootQuestion(index) {
                const question = kahootQuestions[index];
                
                // Update question text and number
                document.getElementById('kahoot-question-text').textContent = question.question;
                document.getElementById('current-kahoot-question').textContent = index + 1;
                
                // Update options
                const options = document.querySelectorAll('.kahoot-option');
                options.forEach((option, i) => {
                    option.textContent = question.options[i];
                    option.classList.remove('opacity-50');
                    option.addEventListener('click', handleKahootAnswer, { once: true });
                });
                
                // Hide feedback
                document.getElementById('kahoot-feedback').classList.add('hidden');
                
                // Start timer
                kahootTimeLeft = QUESTION_TIME;
                updateKahootTimer();
                
                clearInterval(kahootTimer);
                kahootTimer = setInterval(() => {
                    kahootTimeLeft--;
                    updateKahootTimer();
                    
                    if (kahootTimeLeft <= 0) {
                        clearInterval(kahootTimer);
                        timeUpKahoot();
                    }
                }, 1000);
            }
            
            function updateKahootTimer() {
                const percent = (kahootTimeLeft / QUESTION_TIME) * 100;
                document.getElementById('kahoot-timer-progress').style.width = `${percent}%`;
                
                // Change color as time decreases
                if (percent > 60) {
                    document.getElementById('kahoot-timer-progress').style.backgroundColor = 'var(--primary)';
                } else if (percent > 30) {
                    document.getElementById('kahoot-timer-progress').style.backgroundColor = 'var(--warning)';
                } else {
                    document.getElementById('kahoot-timer-progress').style.backgroundColor = 'var(--error)';
                }
            }
            
            function handleKahootAnswer(event) {
                clearInterval(kahootTimer);
                
                const selectedIndex = parseInt(event.currentTarget.getAttribute('data-index'));
                const correctIndex = kahootQuestions[currentKahootQuestion].correctIndex;
                const feedbackElement = document.getElementById('kahoot-feedback');
                
                // Disable all options
                document.querySelectorAll('.kahoot-option').forEach(option => {
                    if (parseInt(option.getAttribute('data-index')) !== selectedIndex) {
                        option.classList.add('opacity-50');
                    }
                    option.removeEventListener('click', handleKahootAnswer);
                });
                
                if (selectedIndex === correctIndex) {
                    // Calculate points based on time left (faster = more points)
                    const points = Math.floor(500 + (kahootTimeLeft / QUESTION_TIME) * 500);
                    kahootScore += points;
                    
                    // Update score display
                    document.getElementById('kahoot-score').textContent = kahootScore;
                    
                    // Show feedback
                    feedbackElement.textContent = `Correct! +${points} points`;
                    feedbackElement.className = 'mt-6 p-4 rounded-lg text-center bg-green-100 text-green-800';
                    feedbackElement.classList.remove('hidden');
                    
                    // Confetti for correct answer
                    confetti({
                        particleCount: 100,
                        spread: 70,
                        origin: { y: 0.6 }
                    });
                } else {
                    // Show feedback
                    feedbackElement.textContent = `Incorrect! The correct answer was: ${kahootQuestions[currentKahootQuestion].options[correctIndex]}`;
                    feedbackElement.className = 'mt-6 p-4 rounded-lg text-center bg-red-100 text-red-800';
                    feedbackElement.classList.remove('hidden');
                }
                
                // Move to next question after delay
                setTimeout(() => {
                    currentKahootQuestion++;
                    if (currentKahootQuestion < kahootQuestions.length) {
                        showKahootQuestion(currentKahootQuestion);
                    } else {
                        showKahootResults();
                    }
                }, 3000);
            }
            
            function timeUpKahoot() {
                const feedbackElement = document.getElementById('kahoot-feedback');
                const correctIndex = kahootQuestions[currentKahootQuestion].correctIndex;
                
                // Disable all options
                document.querySelectorAll('.kahoot-option').forEach(option => {
                    option.classList.add('opacity-50');
                    option.removeEventListener('click', handleKahootAnswer);
                });
                
                // Show feedback
                feedbackElement.textContent = `Time's up! The correct answer was: ${kahootQuestions[currentKahootQuestion].options[correctIndex]}`;
                feedbackElement.className = 'mt-6 p-4 rounded-lg text-center bg-yellow-100 text-yellow-800';
                feedbackElement.classList.remove('hidden');
                
                // Move to next question after delay
                setTimeout(() => {
                    currentKahootQuestion++;
                    if (currentKahootQuestion < kahootQuestions.length) {
                        showKahootQuestion(currentKahootQuestion);
                    } else {
                        showKahootResults();
                    }
                }, 3000);
            }
            
            function showKahootResults() {
                document.getElementById('kahoot-game').classList.add('hidden');
                document.getElementById('kahoot-results').classList.remove('hidden');
                
                // Update final score
                document.getElementById('final-kahoot-score').textContent = kahootScore;
                document.getElementById('leaderboard-score').textContent = kahootScore;
                
                // Store score
                localStorage.setItem('kahootScore', kahootScore);
                document.getElementById('final-game-score').textContent = kahootScore;
                
                // Confetti celebration
                if (kahootScore > 7500) {
                    confetti({
                        particleCount: 200,
                        spread: 120,
                        origin: { y: 0.6 }
                    });
                }
            }
            
            document.getElementById('restart-kahoot').addEventListener('click', function() {
                // Reset Kahoot state
                currentKahootQuestion = 0;
                kahootScore = 0;
                document.getElementById('kahoot-score').textContent = 0;
                
                // Show intro screen
                document.getElementById('kahoot-results').classList.add('hidden');
                document.getElementById('kahoot-intro').classList.remove('hidden');
            });
            
            // Story challenge functionality
            document.getElementById('save-story').addEventListener('click', function() {
                const storyText = document.getElementById('story-area').value.trim();
                
                if (storyText.length > 20) {
                    // Save story to localStorage
                    localStorage.setItem('adolescentBrainStory', storyText);
                    
                    // Show feedback
                    document.getElementById('story-feedback').classList.remove('hidden');
                    
                    // Confetti celebration
                    confetti({
                        particleCount: 100,
                        spread: 70,
                        origin: { y: 0.6 }
                    });
                } else {
                    alert('Please write a more detailed story before saving.');
                }
            });
            
            // Load story from localStorage if it exists
            const savedStory = localStorage.getItem('adolescentBrainStory');
            if (savedStory) {
                document.getElementById('story-area').value = savedStory;
                document.getElementById('story-feedback').classList.remove('hidden');
            }
            
            // Start the presentation
            document.getElementById('restart-presentation').addEventListener('click', function() {
                // Reset presentation
                localStorage.removeItem('currentSlide');
                localStorage.removeItem('quizScore');
                localStorage.removeItem('exerciseScore');
                localStorage.removeItem('kahootScore');
                
                // Go to first slide
                showSlide(1);
            });
            
            // Initialize the presentation
            initializePresentation();
            
            // Load scores if they exist
            const savedQuizScore = localStorage.getItem('quizScore');
            if (savedQuizScore) {
                document.getElementById('final-quiz-score').textContent = `${savedQuizScore}/5`;
            }
            
            const savedExerciseScore = localStorage.getItem('exerciseScore');
            if (savedExerciseScore) {
                document.getElementById('final-exercise-score').textContent = `${savedExerciseScore}/3`;
            }
            
            const savedKahootScore = localStorage.getItem('kahootScore');
            if (savedKahootScore) {
                document.getElementById('final-game-score').textContent = savedKahootScore;
            }
        });
    </script>
</body>
</html>

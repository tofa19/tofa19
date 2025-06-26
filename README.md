import React, { useState, useEffect, useRef } from 'react';
import {
  Laptop, Code, Terminal, Palette, Cloud, Gamepad, Lock,
  Linkedin, Mail, Github,
  Star, Trophy, Flame, ChartBar, Globe
} from 'lucide-react';

const App = () => {
  const [typedText, setTypedText] = useState('');
  const aboutMeText = "I'm a final-year Computer Science student passionate about:";
  const typingSpeed = 50;

  useEffect(() => {
    let i = 0;
    const typeEffect = setInterval(() => {
      if (i < aboutMeText.length) {
        setTypedText(prev => prev + aboutMeText.charAt(i));
        i++;
      } else {
        clearInterval(typeEffect);
      }
    }, typingSpeed);

    return () => clearInterval(typeEffect);
  }, []);

  const techStack = [
    { icon: <img src="https://skillicons.dev/icons?i=py" alt="Python" className="w-8 h-8 md:w-10 md:h-10" />, name: 'Python' },
    { icon: <img src="https://skillicons.dev/icons?i=c,cpp" alt="C/C++" className="w-8 h-8 md:w-10 md:h-10" />, name: 'C/C++' },
    { icon: <img src="https://skillicons.dev/icons?i=java" alt="Java" className="w-8 h-8 md:w-10 md:h-10" />, name: 'Java' },
    { icon: <img src="https://skillicons.dev/icons?i=js" alt="JavaScript" className="w-8 h-8 md:w-10 md:h-10" />, name: 'JavaScript' },
    { icon: <img src="https://skillicons.dev/icons?i=html" alt="HTML" className="w-8 h-8 md:w-10 md:h-10" />, name: 'HTML' },
    { icon: <img src="https://skillicons.dev/icons?i=css" alt="CSS" className="w-8 h-8 md:w-10 md:h-10" />, name: 'CSS' },
    { icon: <img src="https://skillicons.dev/icons?i=flutter" alt="Flutter" className="w-8 h-8 md:w-10 md:h-10" />, name: 'Flutter' },
    { icon: <img src="https://skillicons.dev/icons?i=arduino" alt="Arduino" className="w-8 h-8 md:w-10 md:h-10" />, name: 'Arduino' },
    { icon: <img src="https://skillicons.dev/icons?i=dart" alt="Dart" className="w-8 h-8 md:w-10 md:h-10" />, name: 'Dart' },
    { icon: <img src="https://skillicons.dev/icons?i=react" alt="React" className="w-8 h-8 md:w-10 md:h-10" />, name: 'React' },
    { icon: <img src="https://skillicons.dev/icons?i=ts" alt="TypeScript" className="w-8 h-8 md:w-10 md:h-10" />, name: 'TypeScript' },
  ];

  const tools = [
    { icon: <img src="https://skillicons.dev/icons?i=git" alt="Git" className="w-8 h-8 md:w-10 md:h-10" />, name: 'Git' },
    { icon: <img src="https://skillicons.dev/icons?i=linux" alt="Linux" className="w-8 h-8 md:w-10 md:h-10" />, name: 'Linux' },
    { icon: <img src="https://skillicons.dev/icons?i=vscode" alt="VSCode" className="w-8 h-8 md:w-10 md:h-10" />, name: 'VS Code' },
    { icon: <Terminal className="w-8 h-8 md:w-10 md:h-10 text-green-500" />, name: 'Bash' },
    { icon: <Palette className="w-8 h-8 md:w-10 md:h-10 text-purple-500" />, name: 'Figma' },
    { icon: <Cloud className="w-8 h-8 md:w-10 md:h-10 text-gray-500" />, name: 'Vercel' },
  ];

  // Placeholder for GitHub stats data - these would ideally come from an API
  const githubStats = {
    stars: 850,
    commits: 1230,
    prs: 75,
    issues: 40,
    trophies: [
      { name: 'Star Gazer', value: '⭐️x5' },
      { name: 'Public Relations', value: '🗣️' },
      { name: 'Awesome Dev', value: '🌟' }
    ],
    topLangs: [
      { name: 'Python', percentage: 45 },
      { name: 'Java', percentage: 20 },
      { name: 'C++', percentage: 15 },
      { name: 'JavaScript', percentage: 10 },
      { name: 'Other', percentage: 10 },
    ],
  };

  const statItems = [
    { name: 'Total Stars', value: githubStats.stars, icon: <Star className="text-yellow-400" /> },
    { name: 'Total Commits', value: githubStats.commits, icon: <Code className="text-gray-400" /> }, {/* Changed from GitBranch to Code for a Lucide icon */}
    { name: 'Pull Requests', value: githubStats.prs, icon: <Code className="text-teal-400" /> },
    { name: 'Issues Opened', value: githubStats.issues, icon: <Flame className="text-red-400" /> },
  ];

  const projectList = [
    {
      title: 'Ethical AI in Recruitment',
      description: 'A fairness-aware recruitment system using AIF360, SHAP, and CV filtering logic to ensure unbiased candidate selection.',
      link: 'https://github.com/tofa19/ethical-ai-recruitment',
      icon: <Laptop className="text-pink-500" />
    },
    {
      title: 'Capture the King',
      description: 'A Python-based 2-player strategy board game with a custom heuristic AI, special king powers, and Pygame GUI.',
      link: 'https://github.com/tofa19/capture-the-king',
      icon: <Gamepad className="text-purple-500" />
    },
    {
      title: 'Smart Air Monitor IoT',
      description: 'Air quality and ventilation control system using ESP32, Blynk, and real-time sensor data.',
      link: 'https://github.com/tofa19/smart-air-monitor',
      icon: <Globe className="text-green-500" />
    },
    {
      title: 'Smart Energy Manager',
      description: 'Commercial building energy optimization with PIR, LDR, DHT22 sensors, relays, and web alerts.',
      link: 'https://github.com/tofa19/smart-energy-management',
      icon: <Lock className="text-blue-500" />
    },
  ];


  const StatBar = ({ name, value, icon, max = 2000 }) => {
    const [width, setWidth] = useState(0);
    const barRef = useRef(null);

    useEffect(() => {
      const observer = new IntersectionObserver(
        (entries) => {
          entries.forEach((entry) => {
            if (entry.isIntersecting) {
              const percentage = Math.min((value / max) * 100, 100);
              setWidth(percentage);
              observer.unobserve(entry.target);
            }
          });
        },
        { threshold: 0.1 }
      );

      if (barRef.current) {
        observer.observe(barRef.current);
      }

      return () => {
        if (barRef.current) {
          observer.unobserve(barRef.current);
        }
      };
    }, [value, max]);

    return (
      <div className="mb-4">
        <div className="flex items-center justify-between text-gray-300 mb-1">
          <span className="flex items-center gap-2">{icon} {name}</span>
          <span className="font-semibold">{value}</span>
        </div>
        <div className="w-full bg-gray-700 rounded-full h-2.5">
          <div
            ref={barRef}
            className="bg-blue-500 h-2.5 rounded-full transition-all duration-1000 ease-out"
            style={{ width: `${width}%` }}
          ></div>
        </div>
      </div>
    );
  };

  const LanguageCircle = ({ name, percentage, color }) => {
    const radius = 50;
    const circumference = 2 * Math.PI * radius;
    const [strokeDashoffset, setStrokeDashoffset] = useState(circumference);
    const circleRef = useRef(null);

    useEffect(() => {
      const observer = new IntersectionObserver(
        (entries) => {
          entries.forEach((entry) => {
            if (entry.isIntersecting) {
              setStrokeDashoffset(circumference - (percentage / 100) * circumference);
              observer.unobserve(entry.target);
            }
          });
        },
        { threshold: 0.1 }
      );

      if (circleRef.current) {
        observer.observe(circleRef.current);
      }

      return () => {
        if (circleRef.current) {
          observer.unobserve(circleRef.current);
        }
      };
    }, [percentage, circumference]);

    return (
      <div className="flex flex-col items-center p-2">
        <div className="relative w-28 h-28">
          <svg className="w-full h-full transform -rotate-90">
            <circle
              className="text-gray-700"
              strokeWidth="10"
              stroke="currentColor"
              fill="transparent"
              r={radius}
              cx="50%"
              cy="50%"
            />
            <circle
              ref={circleRef}
              className="transition-all duration-1000 ease-out"
              strokeWidth="10"
              strokeDasharray={circumference}
              strokeDashoffset={strokeDashoffset}
              strokeLinecap="round"
              stroke={color}
              fill="transparent"
              r={radius}
              cx="50%"
              cy="50%"
            />
          </svg>
          <div className="absolute top-0 left-0 w-full h-full flex items-center justify-center text-white text-lg font-bold">
            {percentage}%
          </div>
        </div>
        <span className="mt-2 text-sm text-gray-300">{name}</span>
      </div>
    );
  };


  return (
    <div className="min-h-screen bg-gray-900 text-white font-inter">
      {/* Banner Section */}
      <div className="relative w-full h-48 md:h-60 overflow-hidden rounded-b-2xl shadow-lg">
        <img
          src="https://capsule-render.vercel.app/api?type=waving&color=0:00BFFF,100:1E90FF&height=200&section=header&text=Hi%20👋%2C%20I'm%20Toufique%20Ahamed&fontSize=40&fontColor=ffffff&animation=fadeIn&stroke=false&strokeWidth=0"
          alt="Banner"
          className="w-full h-full object-cover animate-fade-in"
        />
        <style>{`
          @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
          }
          .animate-fade-in {
            animation: fadeIn 1s ease-out forwards;
          }
        `}</style>
      </div>

      <main className="container mx-auto p-6 md:p-10 max-w-4xl">
        {/* About Me Section */}
        <section className="my-10 p-6 bg-gray-800 rounded-xl shadow-lg animate-slide-in-up">
          <h2 className="text-3xl font-bold text-blue-400 mb-4 flex items-center">
            <Laptop className="mr-3" /> About Me
          </h2>
          <p className="text-lg text-gray-300 mb-2 typewriter">
            {typedText}
          </p>
          <ul className="list-disc list-inside text-gray-400 text-md pl-4">
            <li className="mb-1 animate-fade-in-delay-1">🤖 Ethical AI and Fair Machine Learning</li>
            <li className="mb-1 animate-fade-in-delay-2">🌐 Smart IoT Systems (Air Quality Monitoring, Energy Management)</li>
            <li className="mb-1 animate-fade-in-delay-3">🎮 Game Development with custom rules and AI opponents</li>
            <li className="mb-1 animate-fade-in-delay-4">🔐 System-level apps, networking projects, and automation tools</li>
          </ul>
          <p className="mt-4 text-gray-300 animate-fade-in-delay-5">
            I enjoy solving real-world problems using code, working on cool tech projects, and sharing knowledge with others.
          </p>
          <style>{`
            .typewriter::after {
              content: '|';
              animation: blink-caret 0.75s step-end infinite;
            }
            @keyframes blink-caret {
              from, to { border-color: transparent }
              50% { border-color: white; }
            }
            @keyframes slideInUp {
              from { opacity: 0; transform: translateY(20px); }
              to { opacity: 1; transform: translateY(0); }
            }
            .animate-slide-in-up {
              animation: slideInUp 0.8s ease-out forwards;
            }
            .animate-fade-in-delay-1 { animation: fadeIn 0.6s ease-out forwards 0.3s; opacity: 0; }
            .animate-fade-in-delay-2 { animation: fadeIn 0.6s ease-out forwards 0.6s; opacity: 0; }
            .animate-fade-in-delay-3 { animation: fadeIn 0.6s ease-out forwards 0.9s; opacity: 0; }
            .animate-fade-in-delay-4 { animation: fadeIn 0.6s ease-out forwards 1.2s; opacity: 0; }
            .animate-fade-in-delay-5 { animation: fadeIn 0.6s ease-out forwards 1.5s; opacity: 0; }
          `}</style>
        </section>

        {/* Tech Stack Section */}
        <section className="my-10 p-6 bg-gray-800 rounded-xl shadow-lg animate-slide-in-up-delay-1">
          <h2 className="text-3xl font-bold text-blue-400 mb-6 flex items-center">
            <Code className="mr-3" /> Tech Stack
          </h2>
          <div className="grid grid-cols-3 sm:grid-cols-4 lg:grid-cols-6 gap-6 justify-items-center">
            {techStack.map((item, index) => (
              <div
                key={item.name}
                className="flex flex-col items-center p-3 rounded-lg hover:bg-gray-700 transition-all duration-300 transform hover:scale-110 animate-fade-in-stagger"
                style={{ animationDelay: `${0.1 * index}s` }}
              >
                {item.icon}
                <span className="mt-2 text-sm text-gray-300 text-center">{item.name}</span>
              </div>
            ))}
          </div>

          <h3 className="text-2xl font-bold text-blue-300 mt-10 mb-6 flex items-center">
            <Terminal className="mr-3" /> Tools
          </h3>
          <div className="grid grid-cols-3 sm:grid-cols-4 lg:grid-cols-6 gap-6 justify-items-center">
            {tools.map((item, index) => (
              <div
                key={item.name}
                className="flex flex-col items-center p-3 rounded-lg hover:bg-gray-700 transition-all duration-300 transform hover:scale-110 animate-fade-in-stagger"
                style={{ animationDelay: `${0.1 * (techStack.length + index)}s` }}
              >
                {item.icon}
                <span className="mt-2 text-sm text-gray-300 text-center">{item.name}</span>
              </div>
            ))}
          </div>
          <style>{`
            .animate-slide-in-up-delay-1 { animation: slideInUp 0.8s ease-out forwards 0.5s; opacity: 0; }
            .animate-fade-in-stagger {
              animation: fadeIn 0.5s ease-out forwards;
              opacity: 0;
            }
          `}</style>
        </section>

        {/* GitHub Stats Section */}
        <section className="my-10 p-6 bg-gray-800 rounded-xl shadow-lg animate-slide-in-up-delay-2">
          <h2 className="text-3xl font-bold text-blue-400 mb-6 flex items-center">
            <ChartBar className="mr-3" /> GitHub Stats
          </h2>
          <div className="grid grid-cols-1 md:grid-cols-2 gap-8">
            {/* Stat Bars */}
            <div className="space-y-4">
              {statItems.map((item, index) => (
                <StatBar key={index} {...item} />
              ))}
            </div>

            {/* Top Languages Circle Chart */}
            <div>
              <h3 className="text-xl font-semibold text-gray-300 mb-4">Top Languages</h3>
              <div className="flex flex-wrap justify-center gap-4">
                {githubStats.topLangs.map((lang, index) => (
                  <LanguageCircle
                    key={lang.name}
                    name={lang.name}
                    percentage={lang.percentage}
                    color={['#f1e05a', '#b07219', '#555555', '#e34c26', '#3572A5'][index % 5]} // Example colors
                  />
                ))}
              </div>
            </div>
          </div>

          {/* GitHub Trophies (simulated) */}
          <div className="mt-10">
            <h3 className="text-xl font-semibold text-gray-300 mb-4 flex items-center">
              <Trophy className="mr-2 text-yellow-500" /> My Trophies
            </h3>
            <div className="flex flex-wrap justify-center gap-4">
              {githubStats.trophies.map((trophy, index) => (
                <div
                  key={index}
                  className="bg-gray-700 p-4 rounded-xl shadow-md flex flex-col items-center transition-transform transform hover:scale-105 animate-fade-in-stagger"
                  style={{ animationDelay: `${0.1 * index}s` }}
                >
                  <span className="text-4xl mb-2">{trophy.value}</span>
                  <span className="text-sm text-gray-300">{trophy.name}</span>
                </div>
              ))}
            </div>
          </div>
          <style>{`
            .animate-slide-in-up-delay-2 { animation: slideInUp 0.8s ease-out forwards 1s; opacity: 0; }
          `}</style>
        </section>

        {/* Featured Projects Section */}
        <section className="my-10 p-6 bg-gray-800 rounded-xl shadow-lg animate-slide-in-up-delay-3">
          <h2 className="text-3xl font-bold text-blue-400 mb-6 flex items-center">
            <Gamepad className="mr-3" /> Featured Projects
          </h2>
          <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
            {projectList.map((project, index) => (
              <a
                key={index}
                href={project.link}
                target="_blank"
                rel="noopener noreferrer"
                className="block bg-gray-700 p-5 rounded-lg shadow-md transition-all duration-300 transform hover:scale-105 hover:bg-blue-900 group animate-fade-in-stagger"
                style={{ animationDelay: `${0.1 * index}s` }}
              >
                <div className="flex items-center mb-3">
                  {project.icon}
                  <h3 className="text-xl font-semibold text-white ml-3 group-hover:text-blue-200">
                    {project.title}
                  </h3>
                </div>
                <p className="text-gray-300 text-sm group-hover:text-blue-100">
                  {project.description}
                </p>
              </a>
            ))}
          </div>
          <style>{`
            .animate-slide-in-up-delay-3 { animation: slideInUp 0.8s ease-out forwards 1.5s; opacity: 0; }
          `}</style>
        </section>

        {/* Connect with Me Section */}
        <section className="my-10 p-6 bg-gray-800 rounded-xl shadow-lg animate-slide-in-up-delay-4">
          <h2 className="text-3xl font-bold text-blue-400 mb-6 flex items-center">
            <Mail className="mr-3" /> Connect with Me
          </h2>
          <div className="flex flex-wrap justify-center gap-4">
            <a
              href="https://linkedin.com/in/toufiqueahamed"
              target="_blank"
              rel="noopener noreferrer"
              className="px-6 py-3 bg-blue-700 rounded-full text-white font-semibold flex items-center gap-2 hover:bg-blue-600 transition-all duration-300 transform hover:scale-105 hover:shadow-lg animate-bounce-in"
            >
              <Linkedin className="w-5 h-5" /> LinkedIn
            </a>
            <a
              href="https://tofa19.github.io"
              target="_blank"
              rel="noopener noreferrer"
              className="px-6 py-3 bg-gray-700 rounded-full text-white font-semibold flex items-center gap-2 hover:bg-gray-600 transition-all duration-300 transform hover:scale-105 hover:shadow-lg animate-bounce-in"
              style={{ animationDelay: '0.1s' }}
            >
              <Github className="w-5 h-5" /> Portfolio
            </a>
            <a
              href="mailto:your.email@example.com"
              className="px-6 py-3 bg-red-700 rounded-full text-white font-semibold flex items-center gap-2 hover:bg-red-600 transition-all duration-300 transform hover:scale-105 hover:shadow-lg animate-bounce-in"
              style={{ animationDelay: '0.2s' }}
            >
              <Mail className="w-5 h-5" /> Email
            </a>
          </div>
          <style>{`
            .animate-slide-in-up-delay-4 { animation: slideInUp 0.8s ease-out forwards 2s; opacity: 0; }
            @keyframes bounceIn {
              0% { opacity: 0; transform: scale(0.3); }
              50% { opacity: 1; transform: scale(1.05); }
              70% { transform: scale(0.9); }
              100% { transform: scale(1); }
            }
            .animate-bounce-in {
              animation: bounceIn 0.8s ease-out forwards;
              opacity: 0;
            }
          `}</style>
        </section>

        {/* Fun Facts Section */}
        <section className="my-10 p-6 bg-gray-800 rounded-xl shadow-lg animate-slide-in-up-delay-5">
          <h2 className="text-3xl font-bold text-blue-400 mb-4 flex items-center">
            <Trophy className="mr-3" /> Fun Facts
          </h2>
          <ul className="list-disc list-inside text-gray-400 text-md pl-4">
            <li className="mb-1 animate-fade-in-delay-1">🛠️ I love mixing tech and creativity in games and projects.</li>
            <li className="mb-1 animate-fade-in-delay-2">🧪 Currently experimenting with AI bias detection and fairness.</li>
            <li className="mb-1 animate-fade-in-delay-3">🌱 Always learning something new—be it electronics, ML, or cloud tools.</li>
          </ul>
          <style>{`
            .animate-slide-in-up-delay-5 { animation: slideInUp 0.8s ease-out forwards 2.5s; opacity: 0; }
          `}</style>
        </section>

      </main>
    </div>
  );
};

export default App;

// App.jsx
import React, { useState, useEffect } from 'react';
import { 
  Menu, X, Download, ArrowRight, Mail, Phone, MapPin,
  Instagram, Facebook, Linkedin, Youtube, Github, Music2,
  Award, Briefcase, GraduationCap, Users, FolderOpen,
  Calendar, ChevronLeft, ChevronRight, ExternalLink
} from 'lucide-react';
import './App.css';

// Data untuk portfolio
const portfolioData = {
  profile: {
    name: "Carissa",
    fullName: "Salsa Carissa",
    title: "Personal Portfolio & Creative Profile",
    description: "Saya adalah seorang pelajar SMKN 42 Jakarta yang aktif dan berjiwa tangguh. Memiliki passion dalam desain kreatif dan pengembangan web.",
    image: "/api/placeholder/400/400",
    stats: [
      { icon: FolderOpen, value: "15+", label: "Project Selesai" },
      { icon: Award, value: "8", label: "Prestasi" },
      { icon: Users, value: "5", label: "Organisasi" },
      { icon: Briefcase, value: "2", label: "Pengalaman" }
    ]
  },
  skills: [
    { name: "Desain Grafis", level: 85 },
    { name: "Fotografi", level: 75 },
    { name: "Web Development", level: 70 },
    { name: "UI/UX Design", level: 80 },
    { name: "Video Editing", level: 65 },
    { name: "Social Media", level: 90 }
  ],
  education: [
    {
      year: "2023 - Sekarang",
      title: "SMKN 42 Jakarta",
      description: "Jurusan Multimedia - Fokus pada desain grafis, fotografi, dan pengembangan web",
      icon: GraduationCap
    },
    {
      year: "2020 - 2023",
      title: "SMP Negeri 123 Jakarta",
      description: "Aktif dalam organisasi siswa dan kegiatan ekstrakurikuler",
      icon: GraduationCap
    }
  ],
  experience: [
    {
      year: "2024 - Sekarang",
      title: "Freelance Designer",
      company: "Self-employed",
      description: "Mengerjakan berbagai proyek desain untuk klien lokal",
      icon: Briefcase
    },
    {
      year: "2023 - 2024",
      title: "Magang Digital Marketing",
      company: "PT Kreatif Digital",
      description: "Membantu tim dalam pembuatan konten visual dan pengelolaan media sosial",
      icon: Briefcase
    }
  ],
  certificates: [
    { title: "Sertifikat Desain Grafis", issuer: "BNSP", year: "2024" },
    { title: "Sertifikat Web Development", issuer: "Dicoding", year: "2024" },
    { title: "Sertifikat Fotografi", issuer: "Canon Academy", year: "2023" }
  ],
  organizations: [
    { title: "OSIS SMKN 42 Jakarta", role: "Anggota Divisi Kreatif", year: "2024 - Sekarang" },
    { title: "Klub Fotografi", role: "Ketua", year: "2023 - 2024" }
  ],
  achievements: [
    { title: "Juara 1 Lomba Desain Poster", event: "FLS2N Jakarta Barat", year: "2024" },
    { title: "Juara 2 Fotografi", event: "Kompetisi Antar Pelajar", year: "2023" },
    { title: "Best Student Project", event: "SMKN 42 Jakarta", year: "2024" }
  ],
  portfolio: [
    {
      id: 1,
      title: "Website Sekolah",
      category: "Website",
      description: "Redesign website sekolah dengan fokus pada UX/UI modern",
      image: "/api/placeholder/400/300",
      tags: ["React", "Tailwind", "UI/UX"]
    },
    {
      id: 2,
      title: "Desain Poster Event",
      category: "Desain",
      description: "Serangkaian poster untuk event sekolah dan komunitas",
      image: "/api/placeholder/400/300",
      tags: ["Photoshop", "Illustrator"]
    },
    {
      id: 3,
      title: "Fotografi Produk",
      category: "Fotografi",
      description: "Sesi fotografi produk untuk brand lokal",
      image: "/api/placeholder/400/300",
      tags: ["Fotografi", "Lightroom"]
    },
    {
      id: 4,
      title: "Aplikasi Mobile",
      category: "Project",
      description: "Prototype aplikasi mobile untuk manajemen tugas",
      image: "/api/placeholder/400/300",
      tags: ["Figma", "UI Design"]
    },
    {
      id: 5,
      title: "Brand Identity",
      category: "Desain",
      description: "Pembuatan logo dan brand guidelines untuk UMKM",
      image: "/api/placeholder/400/300",
      tags: ["Logo", "Branding"]
    },
    {
      id: 6,
      title: "Video Cinematic",
      category: "Project",
      description: "Video profile untuk acara sekolah",
      image: "/api/placeholder/400/300",
      tags: ["Premiere Pro", "After Effects"]
    }
  ],
  photos: Array.from({ length: 12 }, (_, i) => ({
    id: i + 1,
    title: `Foto ${i + 1}`,
    image: `/api/placeholder/${400 + (i % 3) * 100}/${300 + (i % 4) * 100}`,
    category: ['Acara', 'Portrait', 'Alam', 'Urban'][i % 4]
  })),
  articles: [
    {
      id: 1,
      title: "Tips Memulai Karir di Dunia Kreatif",
      date: "2025-01-15",
      category: "Karir",
      summary: "Pelajari langkah-langkah penting untuk memulai karir di industri kreatif sebagai pelajar",
      image: "/api/placeholder/400/250",
      readTime: "5 min read"
    },
    {
      id: 2,
      title: "Mengenal Dasar-Dasar Desain Grafis",
      date: "2025-01-10",
      category: "Desain",
      summary: "Panduan lengkap untuk pemula yang ingin belajar desain grafis dari nol",
      image: "/api/placeholder/400/250",
      readTime: "8 min read"
    },
    {
      id: 3,
      title: "Pengalaman Magang di Industri Kreatif",
      date: "2024-12-28",
      category: "Pengalaman",
      summary: "Berbagi pengalaman dan pelajaran berharga selama magang di perusahaan kreatif",
      image: "/api/placeholder/400/250",
      readTime: "6 min read"
    },
    {
      id: 4,
      title: "Tools Wajib untuk Content Creator",
      date: "2024-12-20",
      category: "Tools",
      summary: "Rekomendasi tools terbaik yang harus dimiliki content creator modern",
      image: "/api/placeholder/400/250",
      readTime: "4 min read"
    }
  ],
  socialMedia: [
    { name: "Instagram", icon: Instagram, handle: "@salsa.carissa", link: "https://instagram.com/salsa.carissa", color: "from-pink-500 to-purple-600" },
    { name: "TikTok", icon: Music2, handle: "@salsa.creative", link: "https://tiktok.com/@salsa.creative", color: "from-gray-800 to-gray-900" },
    { name: "Facebook", icon: Facebook, handle: "Salsa Carissa", link: "https://facebook.com/salsa.carissa", color: "from-blue-500 to-blue-700" },
    { name: "LinkedIn", icon: Linkedin, handle: "Salsa Carissa", link: "https://linkedin.com/in/salsa-carissa", color: "from-blue-600 to-blue-800" },
    { name: "YouTube", icon: Youtube, handle: "Salsa Creative", link: "https://youtube.com/@salsacreative", color: "from-red-500 to-red-700" },
    { name: "GitHub", icon: Github, handle: "@salsacarissa", link: "https://github.com/salsacarissa", color: "from-gray-600 to-gray-800" }
  ]
};

// Komponen Navbar
const Navbar = ({ activeSection, setActiveSection, isMenuOpen, setIsMenuOpen }) => {
  const menuItems = [
    'Beranda', 'Tentang', 'CV', 'Karya', 'Foto', 'Artikel', 'Media', 'Kontak'
  ];

  const scrollToSection = (section) => {
    const element = document.getElementById(section.toLowerCase());
    if (element) {
      element.scrollIntoView({ behavior: 'smooth' });
      setActiveSection(section);
      setIsMenuOpen(false);
    }
  };

  return (
    <nav className="fixed top-0 left-0 right-0 bg-white/80 backdrop-blur-lg border-b border-gray-100 z-50">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="flex justify-between items-center h-16">
          <div className="flex items-center">
            <span className="text-2xl font-bold text-gray-900">Salsa<span className="text-blue-600">.</span></span>
          </div>
          
          {/* Desktop Navigation */}
          <div className="hidden md:flex items-center space-x-8">
            {menuItems.map((item) => (
              <button
                key={item}
                onClick={() => scrollToSection(item)}
                className={`text-sm font-medium transition-colors duration-200 ${
                  activeSection === item
                    ? 'text-blue-600'
                    : 'text-gray-600 hover:text-gray-900'
                }`}
              >
                {item}
              </button>
            ))}
          </div>

          {/* Mobile Menu Button */}
          <button
            onClick={() => setIsMenuOpen(!isMenuOpen)}
            className="md:hidden p-2 rounded-lg hover:bg-gray-100 transition-colors"
          >
            {isMenuOpen ? <X size={24} /> : <Menu size={24} />}
          </button>
        </div>
      </div>

      {/* Mobile Navigation */}
      {isMenuOpen && (
        <div className="md:hidden bg-white border-t border-gray-100">
          <div className="px-2 pt-2 pb-3 space-y-1">
            {menuItems.map((item) => (
              <button
                key={item}
                onClick={() => scrollToSection(item)}
                className={`block w-full text-left px-3 py-2 rounded-lg text-base font-medium transition-colors ${
                  activeSection === item
                    ? 'bg-blue-50 text-blue-600'
                    : 'text-gray-600 hover:bg-gray-50'
                }`}
              >
                {item}
              </button>
            ))}
          </div>
        </div>
      )}
    </nav>
  );
};

// Komponen Beranda
const Home = () => {
  return (
    <section id="beranda" className="min-h-screen flex items-center pt-20 pb-12">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
          <div className="space-y-8 animate-fade-in">
            <div className="space-y-4">
              <h1 className="text-5xl sm:text-6xl font-bold text-gray-900">
                Carissa
              </h1>
              <p className="text-xl text-blue-600 font-medium">
                Personal Portfolio & Creative Profile
              </p>
              <p className="text-gray-600 text-lg leading-relaxed max-w-xl">
                Saya adalah seorang pelajar SMKN 42 Jakarta yang aktif dan berjiwa tangguh. 
                Memiliki passion dalam dunia kreatif dan teknologi.
              </p>
            </div>
            
            <div className="flex flex-wrap gap-4">
              <button className="group px-6 py-3 bg-gray-900 text-white rounded-lg hover:bg-gray-800 transition-all duration-300 flex items-center gap-2 hover:shadow-lg">
                <FolderOpen size={20} />
                Lihat Hasil Karya
                <ArrowRight size={16} className="group-hover:translate-x-1 transition-transform" />
              </button>
              <button className="px-6 py-3 border-2 border-gray-200 text-gray-700 rounded-lg hover:border-gray-900 hover:text-gray-900 transition-all duration-300 flex items-center gap-2">
                <Download size={20} />
                Download CV
              </button>
            </div>

            <div className="flex items-center gap-4 text-sm text-gray-500">
              <span className="flex items-center gap-2">
                <Mail size={16} />
                salsa.carissa@email.com
              </span>
              <span className="flex items-center gap-2">
                <MapPin size={16} />
                Jakarta, Indonesia
              </span>
            </div>
          </div>

          <div className="relative animate-fade-in-delay">
            <div className="relative w-72 h-72 sm:w-96 sm:h-96 mx-auto">
              <div className="absolute inset-0 bg-gradient-to-br from-blue-400 to-blue-600 rounded-full opacity-20 blur-2xl"></div>
              <div className="relative w-full h-full rounded-full overflow-hidden border-4 border-white shadow-2xl">
                <img 
                  src={portfolioData.profile.image}
                  alt="Carissa"
                  className="w-full h-full object-cover"
                />
              </div>
              <div className="absolute -bottom-4 -right-4 bg-white p-4 rounded-2xl shadow-xl">
                <div className="flex items-center gap-2">
                  <Award className="text-blue-600" />
                  <div>
                    <p className="font-semibold text-sm">Creative Designer</p>
                    <p className="text-xs text-gray-500">SMKN 42 Jakarta</p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  );
};

// Komponen Tentang
const About = () => {
  return (
    <section id="tentang" className="py-20 bg-gray-50">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="text-center mb-12">
          <h2 className="text-3xl sm:text-4xl font-bold text-gray-900 mb-4">Tentang Saya</h2>
          <div className="w-20 h-1 bg-blue-600 mx-auto"></div>
        </div>

        <div className="grid grid-cols-1 lg:grid-cols-3 gap-8">
          {/* Profile Card */}
          <div className="bg-white rounded-2xl p-8 shadow-sm hover:shadow-md transition-shadow">
            <div className="text-center">
              <img 
                src={portfolioData.profile.image}
                alt="Profile"
                className="w-32 h-32 rounded-full mx-auto mb-4 object-cover border-4 border-gray-100"
              />
              <h3 className="text-xl font-semibold text-gray-900">Salsa Carissa</h3>
              <p className="text-gray-600 mt-1">Creative Designer & Student</p>
            </div>
            <p className="text-gray-600 mt-6 text-center leading-relaxed">
              Saya adalah pelajar SMKN 42 Jakarta yang passionate dalam desain kreatif, 
              fotografi, dan pengembangan web. Aktif dalam berbagai kegiatan dan organisasi sekolah.
            </p>
          </div>

          {/* Skills */}
          <div className="bg-white rounded-2xl p-8 shadow-sm hover:shadow-md transition-shadow">
            <h3 className="text-xl font-semibold text-gray-900 mb-6">Keahlian</h3>
            <div className="space-y-4">
              {portfolioData.skills.map((skill, index) => (
                <div key={index}>
                  <div className="flex justify-between mb-1">
                    <span className="text-sm font-medium text-gray-700">{skill.name}</span>
                    <span className="text-sm text-gray-500">{skill.level}%</span>
                  </div>
                  <div className="h-2 bg-gray-100 rounded-full overflow-hidden">
                    <div 
                      className="h-full bg-blue-600 rounded-full transition-all duration-1000"
                      style={{ width: `${skill.level}%` }}
                    ></div>
                  </div>
                </div>
              ))}
            </div>
          </div>

          {/* Stats */}
          <div className="space-y-4">
            {portfolioData.profile.stats.map((stat, index) => (
              <div key={index} className="bg-white rounded-2xl p-6 shadow-sm hover:shadow-md transition-shadow">
                <div className="flex items-center gap-4">
                  <div className="p-3 bg-blue-50 rounded-xl">
                    <stat.icon className="text-blue-600" size={24} />
                  </div>
                  <div>
                    <p className="text-2xl font-bold text-gray-900">{stat.value}</p>
                    <p className="text-sm text-gray-600">{stat.label}</p>
                  </div>
                </div>
              </div>
            ))}
          </div>
        </div>
      </div>
    </section>
  );
};

// Komponen CV
const CV = () => {
  return (
    <section id="cv" className="py-20">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="text-center mb-12">
          <h2 className="text-3xl sm:text-4xl font-bold text-gray-900 mb-4">Curriculum Vitae</h2>
          <div className="w-20 h-1 bg-blue-600 mx-auto"></div>
          <button className="mt-6 px-6 py-3 bg-gray-900 text-white rounded-lg hover:bg-gray-800 transition-all duration-300 flex items-center gap-2 mx-auto hover:shadow-lg">
            <Download size={20} />
            Download CV PDF
          </button>
        </div>

        <div className="grid grid-cols-1 lg:grid-cols-2 gap-8">
          {/* Left Column */}
          <div className="space-y-8">
            {/* Education */}
            <div className="bg-white rounded-2xl p-8 shadow-sm">
              <h3 className="text-xl font-semibold text-gray-900 mb-6 flex items-center gap-2">
                <GraduationCap className="text-blue-600" />
                Pendidikan
              </h3>
              <div className="space-y-6">
                {portfolioData.education.map((edu, index) => (
                  <div key={index} className="relative pl-8 border-l-2 border-gray-100">
                    <div className="absolute left-[-9px] top-0 w-4 h-4 bg-blue-600 rounded-full border-2 border-white"></div>
                    <p className="text-sm text-gray-500">{edu.year}</p>
                    <h4 className="font-semibold text-gray-900 mt-1">{edu.title}</h4>
                    <p className="text-gray-600 text-sm mt-1">{edu.description}</p>
                  </div>
                ))}
              </div>
            </div>

            {/* Experience */}
            <div className="bg-white rounded-2xl p-8 shadow-sm">
              <h3 className="text-xl font-semibold text-gray-900 mb-6 flex items-center gap-2">
                <Briefcase className="text-blue-600" />
                Pengalaman
              </h3>
              <div className="space-y-6">
                {portfolioData.experience.map((exp, index) => (
                  <div key={index} className="relative pl-8 border-l-2 border-gray-100">
                    <div className="absolute left-[-9px] top-0 w-4 h-4 bg-blue-600 rounded-full border-2 border-white"></div>
                    <p className="text-sm text-gray-500">{exp.year}</p>
                    <h4 className="font-semibold text-gray-900 mt-1">{exp.title}</h4>
                    <p className="text-blue-600 text-sm">{exp.company}</p>
                    <p className="text-gray-600 text-sm mt-1">{exp.description}</p>
                  </div>
                ))}
              </div>
            </div>
          </div>

          {/* Right Column */}
          <div className="space-y-8">
            {/* Certificates */}
            <div className="bg-white rounded-2xl p-8 shadow-sm">
              <h3 className="text-xl font-semibold text-gray-900 mb-6 flex items-center gap-2">
                <Award className="text-blue-600" />
                Sertifikat
              </h3>
              <div className="space-y-4">
                {portfolioData.certificates.map((cert, index) => (
                  <div key={index} className="flex items-start gap-3 p-3 hover:bg-gray-50 rounded-lg transition-colors">
                    <Award size={20} className="text-blue-600 mt-1" />
                    <div>
                      <h4 className="font-semibold text-gray-900">{cert.title}</h4>
                      <p className="text-sm text-gray-600">{cert.issuer} • {cert.year}</p>
                    </div>
                  </div>
                ))}
              </div>
            </div>

            {/* Organizations */}
            <div className="bg-white rounded-2xl p-8 shadow-sm">
              <h3 className="text-xl font-semibold text-gray-900 mb-6 flex items-center gap-2">
                <Users className="text-blue-600" />
                Organisasi
              </h3>
              <div className="space-y-4">
                {portfolioData.organizations.map((org, index) => (
                  <div key={index} className="flex items-start gap-3 p-3 hover:bg-gray-50 rounded-lg transition-colors">
                    <Users size={20} className="text-blue-600 mt-1" />
                    <div>
                      <h4 className="font-semibold text-gray-900">{org.title}</h4>
                      <p className="text-sm text-gray-600">{org.role} • {org.year}</p>
                    </div>
                  </div>
                ))}
              </div>
            </div>

            {/* Achievements */}
            <div className="bg-white rounded-2xl p-8 shadow-sm">
              <h3 className="text-xl font-semibold text-gray-900 mb-6 flex items-center gap-2">
                <Award className="text-blue-600" />
                Prestasi
              </h3>
              <div className="space-y-4">
                {portfolioData.achievements.map((ach, index) => (
                  <div key={index} className="flex items-start gap-3 p-3 hover:bg-gray-50 rounded-lg transition-colors">
                    <Award size={20} className="text-blue-600 mt-1" />
                    <div>
                      <h4 className="font-semibold text-gray-900">{ach.title}</h4>
                      <p className="text-sm text-gray-600">{ach.event} • {ach.year}</p>
                    </div>
                  </div>
                ))}
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  );
};

// Komponen Portfolio
const Portfolio = () => {
  const [activeFilter, setActiveFilter] = useState('Semua');
  const filters = ['Semua', 'Website', 'Desain', 'Fotografi', 'Project', 'Lainnya'];
  
  const filteredPortfolio = activeFilter === 'Semua' 
    ? portfolioData.portfolio 
    : portfolioData.portfolio.filter(item => item.category === activeFilter);

  return (
    <section id="karya" className="py-20 bg-gray-50">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="text-center mb-12">
          <h2 className="text-3xl sm:text-4xl font-bold text-gray-900 mb-4">Hasil Karya</h2>
          <div className="w-20 h-1 bg-blue-600 mx-auto"></div>
        </div>

        {/* Filter Buttons */}
        <div className="flex flex-wrap justify-center gap-3 mb-8">
          {filters.map((filter) => (
            <button
              key={filter}
              onClick={() => setActiveFilter(filter)}
              className={`px-5 py-2 rounded-full text-sm font-medium transition-all duration-300 ${
                activeFilter === filter
                  ? 'bg-gray-900 text-white'
                  : 'bg-white text-gray-600 hover:bg-gray-100'
              }`}
            >
              {filter}
            </button>
          ))}
        </div>

        {/* Portfolio Grid */}
        <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
          {filteredPortfolio.map((item) => (
            <div 
              key={item.id}
              className="group bg-white rounded-2xl overflow-hidden shadow-sm hover:shadow-xl transition-all duration-300"
            >
              <div className="relative overflow-hidden">
                <img 
                  src={item.image}
                  alt={item.title}
                  className="w-full h-64 object-cover group-hover:scale-110 transition-transform duration-500"
                />
                <div className="absolute inset-0 bg-black bg-opacity-0 group-hover:bg-opacity-40 transition-all duration-300 flex items-center justify-center opacity-0 group-hover:opacity-100">
                  <button className="px-6 py-3 bg-white text-gray-900 rounded-lg font-medium transform translate-y-4 group-hover:translate-y-0 transition-all duration-300">
                    Lihat Detail
                  </button>
                </div>
              </div>
              <div className="p-6">
                <div className="flex items-center justify-between mb-2">
                  <h3 className="text-lg font-semibold text-gray-900">{item.title}</h3>
                  <span className="text-xs px-3 py-1 bg-blue-50 text-blue-600 rounded-full">
                    {item.category}
                  </span>
                </div>
                <p className="text-gray-600 text-sm mb-4">{item.description}</p>
                <div className="flex flex-wrap gap-2">
                  {item.tags.map((tag, index) => (
                    <span key={index} className="text-xs px-2 py-1 bg-gray-100 text-gray-600 rounded">
                      {tag}
                    </span>
                  ))}
                </div>
              </div>
            </div>
          ))}
        </div>
      </div>
    </section>
  );
};

// Komponen Foto
const Photos = () => {
  const [selectedPhoto, setSelectedPhoto] = useState(null);

  return (
    <section id="foto" className="py-20">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="text-center mb-12">
          <h2 className="text-3xl sm:text-4xl font-bold text-gray-900 mb-4">Galeri Foto</h2>
          <div className="w-20 h-1 bg-blue-600 mx-auto"></div>
        </div>

        <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4">
          {portfolioData.photos.map((photo) => (
            <div
              key={photo.id}
              onClick={() => setSelectedPhoto(photo)}
              className="group relative overflow-hidden rounded-2xl cursor-pointer"
            >
              <img 
                src={photo.image}
                alt={photo.title}
                className="w-full h-64 object-cover group-hover:scale-110 transition-transform duration-500"
              />
              <div className="absolute inset-0 bg-black bg-opacity-0 group-hover:bg-opacity-30 transition-all duration-300">
                <div className="absolute bottom-0 left-0 right-0 p-4 text-white transform translate-y-full group-hover:translate-y-0 transition-transform duration-300">
                  <p className="font-semibold">{photo.title}</p>
                  <p className="text-sm opacity-90">{photo.category}</p>
                </div>
              </div>
            </div>
          ))}
        </div>
      </div>

      {/* Lightbox */}
      {selectedPhoto && (
        <div 
          className="fixed inset-0 bg-black bg-opacity-90 z-50 flex items-center justify-center p-4"
          onClick={() => setSelectedPhoto(null)}
        >
          <div className="relative max-w-4xl w-full">
            <img 
              src={selectedPhoto.image}
              alt={selectedPhoto.title}
              className="w-full h-auto rounded-lg"
            />
            <button 
              onClick={() => setSelectedPhoto(null)}
              className="absolute top-4 right-4 p-2 bg-white rounded-full hover:bg-gray-100 transition-colors"
            >
              <X size={24} />
            </button>
            <div className="absolute bottom-4 left-4 text-white">
              <h3 className="text-xl font-semibold">{selectedPhoto.title}</h3>
              <p className="text-sm opacity-90">{selectedPhoto.category}</p>
            </div>
          </div>
        </div>
      )}
    </section>
  );
};

// Komponen Artikel
const Articles = () => {
  return (
    <section id="artikel" className="py-20 bg-gray-50">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="text-center mb-12">
          <h2 className="text-3xl sm:text-4xl font-bold text-gray-900 mb-4">Artikel</h2>
          <div className="w-20 h-1 bg-blue-600 mx-auto"></div>
        </div>

        <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
          {portfolioData.articles.map((article) => (
            <article 
              key={article.id}
              className="bg-white rounded-2xl overflow-hidden shadow-sm hover:shadow-xl transition-all duration-300 group"
            >
              <div className="relative overflow-hidden">
                <img 
                  src={article.image}
                  alt={article.title}
                  className="w-full h-56 object-cover group-hover:scale-110 transition-transform duration-500"
                />
                <div className="absolute top-4 left-4">
                  <span className="px-3 py-1 bg-white/90 backdrop-blur text-xs font-medium text-gray-900 rounded-full">
                    {article.category}
                  </span>
                </div>
              </div>
              <div className="p-6">
                <div className="flex items-center gap-3 text-sm text-gray-500 mb-3">
                  <span className="flex items-center gap-1">
                    <Calendar size={14} />
                    {article.date}
                  </span>
                  <span>•</span>
                  <span>{article.readTime}</span>
                </div>
                <h3 className="text-lg font-semibold text-gray-900 mb-2 group-hover:text-blue-600 transition-colors">
                  {article.title}
                </h3>
                <p className="text-gray-600 text-sm mb-4">{article.summary}</p>
                <button className="text-blue-600 font-medium text-sm flex items-center gap-1 hover:gap-2 transition-all">
                  Baca Selengkapnya
                  <ArrowRight size={16} />
                </button>
              </div>
            </article>
          ))}
        </div>
      </div>
    </section>
  );
};

// Komponen Media Sosial
const SocialMedia = () => {
  return (
    <section id="media" className="py-20">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="text-center mb-12">
          <h2 className="text-3xl sm:text-4xl font-bold text-gray-900 mb-4">Media Sosial</h2>
          <div className="w-20 h-1 bg-blue-600 mx-auto"></div>
          <p className="text-gray-600 mt-4">Ikuti saya di media sosial untuk update terbaru</p>
        </div>

        <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
          {portfolioData.socialMedia.map((social, index) => (
            <a
              key={index}
              href={social.link}
              target="_blank"
              rel="noopener noreferrer"
              className="group bg-white rounded-2xl p-8 shadow-sm hover:shadow-xl transition-all duration-300 hover:-translate-y-1"
            >
              <div className={`w-16 h-16 bg-gradient-to-br ${social.color} rounded-2xl flex items-center justify-center mb-4 group-hover:scale-110 transition-transform`}>
                <social.icon className="text-white" size={32} />
              </div>
              <h3 className="text-xl font-semibold text-gray-900 mb-1">{social.name}</h3>
              <p className="text-gray-600">{social.handle}</p>
              <div className="mt-4 flex items-center gap-1 text-blue-600 font-medium text-sm opacity-0 group-hover:opacity-100 transition-opacity">
                Kunjungi
                <ExternalLink size={14} />
              </div>
            </a>
          ))}
        </div>
      </div>
    </section>
  );
};

// Komponen Kontak
const Contact = () => {
  const [formData, setFormData] = useState({
    name: '',
    email: '',
    subject: '',
    message: ''
  });

  const handleSubmit = (e) => {
    e.preventDefault();
    // Handle form submission
    console.log('Form submitted:', formData);
    alert('Pesan berhasil dikirim!');
    setFormData({ name: '', email: '', subject: '', message: '' });
  };

  const handleChange = (e) => {
    setFormData({
      ...formData,
      [e.target.name]: e.target.value
    });
  };

  return (
    <section id="kontak" className="py-20 bg-gray-50">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="text-center mb-12">
          <h2 className="text-3xl sm:text-4xl font-bold text-gray-900 mb-4">Kontak</h2>
          <div className="w-20 h-1 bg-blue-600 mx-auto"></div>
        </div>

        <div className="grid grid-cols-1 lg:grid-cols-2 gap-12">
          {/* Contact Form */}
          <div className="bg-white rounded-2xl p-8 shadow-sm">
            <h3 className="text-xl font-semibold text-gray-900 mb-6">Kirim Pesan</h3>
            <form onSubmit={handleSubmit} className="space-y-4">
              <div>
                <label className="block text-sm font-medium text-gray-700 mb-1">
                  Nama Lengkap
                </label>
                <input
                  type="text"
                  name="name"
                  value={formData.name}
                  onChange={handleChange}
                  required
                  className="w-full px-4 py-3 border border-gray-200 rounded-lg focus:out

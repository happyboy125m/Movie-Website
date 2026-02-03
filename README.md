import React, { useEffect, useState } from 'react';
import axios from 'axios';
import Header from '../components/Header';
import Footer from '../components/Footer';
import CategorySection from '../components/CategorySection';
import MovieCard from '../components/MovieCard';

const HomePage = () => {
  const [categories, setCategories] = useState([]);
  const [featuredMovie, setFeaturedMovie] = useState(null);

  useEffect(() => {
    // Fetch categories and featured movie from backend
    const fetchData = async () => {
      try {
        const catRes = await axios.get('/api/categories');
        setCategories(catRes.data);
        const movieRes = await axios.get('/api/movies/featured');
        setFeaturedMovie(movieRes.data);
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    };
    fetchData();
  }, []);

  return (
    <div className="min-h-screen bg-gray-900 text-white">
      <Header />
      
      {/* Hero Banner */}
      {featuredMovie && (
        <div className="relative h-96 bg-cover bg-center" style={{ backgroundImage: `url(${featuredMovie.poster})` }}>
          <div className="absolute inset-0 bg-black bg-opacity-50 flex items-center justify-center">
            <div className="text-center">
              <h1 className="text-5xl font-bold mb-4">{featuredMovie.title}</h1>
              <p className="text-lg mb-6">{featuredMovie.description}</p>
              <button className="bg-red-600 hover:bg-red-700 px-6 py-3 rounded-lg font-semibold">
                Watch Now
              </button>
            </div>
          </div>
        </div>
      )}

      {/* Categories Sections */}
      <div className="px-8 py-8">
        {categories.map((category) => (
          <CategorySection key={category._id} category={category} />
        ))}
      </div>

      <Footer />
    </div>
  );
};

export default HomePage;

import React, { useEffect, useState } from 'react';
import axios from 'axios';
import { useAuth } from '../hooks/useAuth';

const AdminDashboard = () => {
  const { user } = useAuth();
  const [movies, setMovies] = useState([]);
  const [newMovie, setNewMovie] = useState({ title: '', category: '', servers: [], downloads: [] });

  useEffect(() => {
    if (user?.role !== 'admin') return; // Redirect if not admin
    const fetchMovies = async () => {
      try {
        const res = await axios.get('/api/admin/movies', { headers: { Authorization: `Bearer ${user.token}` } });
        setMovies(res.data);
      } catch (error) {
        console.error('Error fetching movies:', error);
      }
    };
    fetchMovies();
  }, [user]);

  const handleUpload = async () => {
    try {
      await axios.post('/api/admin/movies', newMovie, { headers: { Authorization: `Bearer ${user.token}` } });
      // Refresh list
      setMovies([...movies, newMovie]);
      setNewMovie({ title: '', category: '', servers: [], downloads: [] });
    } catch (error) {
      console.error('Error uploading movie:', error);
    }
  };

  if (user?.role !== 'admin') return <div>Access Denied</div>;

  return (
    <div className="min-h-screen bg-gray-900 text-white p-8">
      <h1 className="text-3xl font-bold mb-8">Admin Dashboard</h1>
      
      {/* Upload Movie Form */}
      <div className="bg-gray-800 p-6 rounded-lg mb-8">
        <h2 className="text-xl mb-4">Upload New Movie</h2>
        <input
          type="text"
          placeholder="Title"
          value={newMovie.title}
          onChange={(e) => setNewMovie({ ...newMovie, title: e.target.value })}
          className="w-full p-2 mb-4 bg-gray-700 rounded"
        />
        <select
          value={newMovie.category}
          onChange={(e) => setNewMovie({ ...newMovie, category: e.target.value })}
          className="w-full p-2 mb-4 bg-gray-700 rounded"
        >
          <option value="">Select Category</option>
          <option value="Movies">Movies</option>
          <option value="18+ Content">18+ Content</option>
          <option value="Anime">Anime</option>
          <option value="K-Drama">K-Drama</option>
          <option value="Netflix Originals">Netflix Originals</option>
        </select>
        {/* Add fields for servers and downloads here */}
        <button onClick={handleUpload} className="bg-red-600 hover:bg-red-700 px-4 py-2 rounded">
          Upload
        </button>
      </div>

      {/* Manage Movies */}
      <div className="bg-gray-800 p-6 rounded-lg">
        <h2 className="text-xl mb-4">Manage Movies</h2>
        <ul>
          {movies.map((movie) => (
            <li key={movie._id} className="flex justify-between items-center mb-2">
              <span>{movie.title}</span>
              <button className="bg-blue-600 hover:bg-blue-700 px-3 py-1 rounded">Edit</button>
              <button className="bg-red-600 hover:bg-red-700 px-3 py-1 rounded">Delete</button>
            </li>
          ))}
        </ul>
      </div>

      {/* Placeholders for Link Shorteners/Ads */}
      <div className="bg-gray-800 p-6 rounded-lg mt-8">
        <h2 className="text-xl mb-4">Link Shorteners & Ads</h2>
        <p>Integrate shorteners and ad management here.</p>
      </div>
    </div>
  );
};

export default AdminDashboard;

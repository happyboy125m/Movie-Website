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

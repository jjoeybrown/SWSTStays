<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="title" content="Southwest Short Term Stays | Luxury Airbnb Management & Real Estate">
  <meta name="description" content="Southwest Short Term Stays offers premier short-term rental management, real estate sales, and luxury home renovations in West Chester, Germantown, Norris Lake, and Red River Gorge. Maximize your property's value with our local expertise.">
  <meta name="keywords" content="Airbnb management, short-term rentals, West Chester real estate, Norris Lake homes, Red River Gorge cabins">
  <title>Southwest Short Term Stays | Luxury Airbnb Management & Real Estate</title>
  <script src="https://cdn.jsdelivr.net/npm/react@18.2.0/umd/react.production.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/react-dom@18.2.0/umd/react-dom.production.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/@babel/standalone@7.20.15/babel.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/emailjs-com@3.2.0/dist/email.min.js"></script>
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body>
  <div id="root"></div>
  <script type="text/babel">
    // Initialize EmailJS with your public key
    // TODO: Replace 'YOUR_EMAILJS_PUBLIC_KEY' with your EmailJS User ID (from EmailJS dashboard > Account > API Keys)
    emailjs.init("YOUR_EMAILJS_PUBLIC_KEY");

    // Main App Component
    const App = () => {
      const [isModalOpen, setIsModalOpen] = React.useState(false);
      const [formData, setFormData] = React.useState({ name: '', email: '', phone: '', message: '' });
      const [error, setError] = React.useState('');

      // Handle modal toggle
      const toggleModal = () => {
        setIsModalOpen(!isModalOpen);
        setError('');
      };

      // Handle input changes
      const handleInputChange = (e) => {
        const { name, value } = e.target;
        setFormData({ ...formData, [name]: value });
        setError('');
      };

      // Validate email format
      const isValidEmail = (email) => {
        const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        return emailRegex.test(email);
      };

      // Handle form submission (sends email via EmailJS)
      const handleSubmit = (e) => {
        e.preventDefault();
        if (!formData.name || !formData.email) {
          setError('Please fill out Name and Email fields');
          return;
        }
        if (!isValidEmail(formData.email)) {
          setError('Please enter a valid email address');
          return;
        }
        // TODO: Replace 'YOUR_SERVICE_ID' and 'YOUR_TEMPLATE_ID' with your EmailJS Service ID and Template ID
        emailjs.send('YOUR_SERVICE_ID', 'YOUR_TEMPLATE_ID', {
          from_name: formData.name,
          from_email: formData.email,
          phone: formData.phone,
          message: formData.message,
          to_email: 'joey.brown@cbishome.com'
        }, 'YOUR_EMAILJS_PUBLIC_KEY')
          .then((response) => {
            console.log('Email sent successfully:', response);
            alert('Thank you! Your request has been sent to Southwest Short Term Stays.');
            setFormData({ name: '', email: '', phone: '', message: '' });
            toggleModal();
          }, (error) => {
            console.error('Email sending failed:', error);
            setError(`Failed to send request: ${error.text || 'Unknown error. Please try again.'}`);
          });
      };

      // Smooth scroll to section
      const scrollToSection = (id) => {
        document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' });
      };

      return (
        <div className="font-sans text-gray-800">
          {/* Navigation Bar */}
          <nav className="bg-blue-900 text-white sticky top-0 z-50 shadow-lg">
            <div className="container mx-auto px-4 py-4 flex justify-between items-center">
              <h1 className="text-2xl font-bold font-[Montserrat]">
                Southwest Short Term Stays
              </h1>
              <ul className="flex space-x-6">
                {['Home', 'About', 'Services', 'Locations', 'Testimonials', 'Contact'].map((item) => (
                  <li key={item}>
                    <button
                      onClick={() => scrollToSection(item.toLowerCase())}
                      className="hover:text-yellow-400 transition-colors"
                      aria-label={`Navigate to ${item} section`}
                    >
                      {item}
                    </button>
                  </li>
                ))}
              </ul>
            </div>
          </nav>

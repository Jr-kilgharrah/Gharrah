npx create-react-app client
cd client
npm install
import React, { useEffect, useState } from "react";
import Header from "./components/Header";
import About from "./components/About";
import Skills from "./components/Skills";
import Experience from "./components/Experience";
import Education from "./components/Education";
import Certifications from "./components/Certifications";
import Projects from "./components/Projects";
import Interests from "./components/Interests";
import Footer from "./components/Footer";
import "./App.css";

function App() {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch("http://localhost:4000/api/resume")
      .then((res) => res.json())
      .then(setData)
      .catch(console.error);
  }, []);

  if (!data) return <p>Loading…</p>;

  return (
    <>
      <Header info={data} />
      <About text={data.about} />
      <Skills list={data.skills} />
      <Experience items={data.experience} />
      <Education items={data.education} />
      <Certifications list={data.certifications} />
      <Projects list={data.projects} />
      <Interests list={data.interests} />
      <Footer />
    </>
  );
}

export default App;
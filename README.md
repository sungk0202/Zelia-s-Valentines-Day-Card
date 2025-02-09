import { useState } from "react";
import { Button } from "@/components/ui/button";
import { motion } from "framer-motion";
import { Mail, X } from "lucide-react";

export default function EnvelopeLetter() {
  const [isOpen, setIsOpen] = useState(false);
  const [showPopup, setShowPopup] = useState(false);
  const [noPosition, setNoPosition] = useState({ x: 0, y: 0 });

  const moveNoButton = () => {
    const newX = Math.random() * 200 - 100;
    const newY = Math.random() * 200 - 100;
    setNoPosition({ x: newX, y: newY });
  };

  return (
    <div className="flex flex-col items-center justify-center min-h-screen gap-4">
      {!isOpen ? (
        <motion.div
          className="cursor-pointer p-12 bg-pink-300 rounded-lg shadow-lg flex flex-col items-center justify-center gap-2"
          whileHover={{ scale: 1.1 }}
          whileTap={{ scale: 0.9 }}
          onClick={() => setIsOpen(true)}
        >
          <Mail size={50} />
          <p className="text-center mt-2 text-lg font-semibold">To Zelia</p>
        </motion.div>
      ) : (
        <motion.div
          className="p-6 bg-white rounded-lg shadow-lg text-center border border-gray-300"
          initial={{ opacity: 0, y: -50 }}
          animate={{ opacity: 1, y: 0 }}
        >
          <p className="text-lg mb-4">❤️ Will you be Sung's Valentine? ❤️</p>
          <div className="flex gap-4 justify-center relative">
            <Button className="bg-green-500 hover:bg-green-600 px-6 py-2 text-white rounded-md" onClick={() => setShowPopup(true)}>Yes</Button>
            <motion.button
              className="bg-red-500 hover:bg-red-600 px-6 py-2 text-white rounded-md"
              onClick={moveNoButton}
              animate={{ x: noPosition.x, y: noPosition.y }}
              transition={{ type: "spring", stiffness: 100 }}
            >
              No
            </motion.button>
          </div>
          <Button
            className="mt-4 bg-gray-400 hover:bg-gray-500"
            onClick={() => setIsOpen(false)}
          >
            <X size={16} className="mr-1" /> Close
          </Button>
        </motion.div>
      )}
      {showPopup && (
        <motion.div 
          className="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50"
          initial={{ opacity: 0 }}
          animate={{ opacity: 1 }}
        >
          <div className="bg-white p-6 rounded-lg shadow-lg text-center">
            <p className="text-xl font-bold">Yippee! 🤭 I can’t wait to celebrate Valentines day with you my lovee! 😘</p>
            <Button className="mt-4 bg-blue-500 hover:bg-blue-600" onClick={() => setShowPopup(false)}>Close</Button>
          </div>
        </motion.div>
      )}
    </div>
  );
}

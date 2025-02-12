"use client"

import { useState } from "react"
import { motion } from "framer-motion"
import { Heart } from "lucide-react"
import confetti from "canvas-confetti"

export default function ValentinesProposal() {
  const [accepted, setAccepted] = useState(false)
  const [noCount, setNoCount] = useState(0)
  const yesButtonSize = noCount * 20 + 100 // Remove the Math.min cap

  const noButtonTexts = [
    "No",
    "Are you sure?",
    "What if I asked really nicely?",
    "Pretty please",
    "But :*(",
    "please babe",
    "No :(",
    "I am going to die",
    "Yep I'm ded",
    "ok ur talking to my ghost",
    "PLEASE",
  ]

  const handleAccept = () => {
    setAccepted(true)
    confetti({
      particleCount: 100,
      spread: 70,
      origin: { y: 0.6 },
    })
  }

  const handleReject = () => {
    setNoCount(noCount + 1)
  }

  return (
    <div className="min-h-screen flex items-center justify-center bg-pink-100">
      <div className="text-center">
        <motion.h1
          className="text-4xl font-bold text-pink-600 mb-8"
          initial={{ opacity: 0, y: -20 }}
          animate={{ opacity: 1, y: 0 }}
          transition={{ duration: 0.5 }}
        >
          {accepted ? "You've made me the happiest person alive!" : "Will you be my Valentine?"}
        </motion.h1>

        {!accepted && (
          <div className="mb-8">
            <img
              src="https://gifdb.com/images/high/cute-love-bear-roses-ou7zho5oosxnpo6k.gif"
              alt="Cute Valentine's Day animation"
              className="w-64 h-64 mx-auto rounded-lg shadow-lg"
            />
          </div>
        )}

        {!accepted && (
          <div className="flex justify-center items-center space-x-4">
            <motion.button
              className="bg-green-500 text-white rounded-full text-xl font-semibold hover:bg-green-600 transition-colors duration-300 overflow-visible"
              whileHover={{ scale: 1.05 }}
              whileTap={{ scale: 0.95 }}
              onClick={handleAccept}
              style={{
                fontSize: `${yesButtonSize}%`,
                padding: "0.75em 1.5em",
                zIndex: 10,
              }}
            >
              Yes
            </motion.button>
            {noCount < noButtonTexts.length - 1 && (
              <motion.button
                className="bg-red-500 text-white px-6 py-3 rounded-full text-xl font-semibold hover:bg-red-600 transition-colors duration-300"
                whileHover={{ scale: 1.05 }}
                whileTap={{ scale: 0.95 }}
                onClick={handleReject}
              >
                {noButtonTexts[noCount]}
              </motion.button>
            )}
            {noCount >= noButtonTexts.length - 1 && (
              <motion.button
                className="bg-purple-500 text-white px-6 py-3 rounded-full text-xl font-semibold hover:bg-purple-600 transition-colors duration-300"
                whileHover={{ scale: 1.05 }}
                whileTap={{ scale: 0.95 }}
                onClick={handleReject}
              >
                {noButtonTexts[noButtonTexts.length - 1]}
              </motion.button>
            )}
          </div>
        )}

        {accepted && (
          <motion.div
            initial={{ scale: 0 }}
            animate={{ scale: 1 }}
            transition={{ type: "spring", stiffness: 260, damping: 20 }}
          >
            <Heart className="w-32 h-32 text-red-500 mx-auto" />
          </motion.div>
        )}
      </div>
    </div>
  )
}


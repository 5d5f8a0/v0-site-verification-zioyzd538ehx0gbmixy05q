https://v0.dev/chat/1Sf5hk5zcI2?b=b_x7eVe9qekzY&p=import React, { useState } from 'react'
import { Card, CardContent, CardHeader, CardTitle } from "@/components/ui/card"
import { Button } from "@/components/ui/button"
import { Input } from "@/components/ui/input"
import { Label } from "@/components/ui/label"
import { Textarea } from "@/components/ui/textarea"
import { toast } from "@/components/ui/use-toast"
import { Github, Play, Save } from 'lucide-react'

export default function PhysicsGitHubIntegration() {
  const [code, setCode] = useState(`import diffractsim
diffractsim.set_backend("CPU") #Change the string to "CUDA" to use GPU acceleration

from diffractsim import MonochromaticField, ApertureFromImage, Lens, mm, nm, cm, FourierPhaseRetrieval

#Generate a Fourier plane phase hologram
PR = FourierPhaseRetrieval(target_amplitude_path = './apertures/dickbutt.jpg', new_size= (400,400), pad = (200,200))
PR.retrieve_phase_mask(max_iter = 200, method = 'Conjugate-Gradient')
PR.save_retrieved_phase_as_image("grating holo.jpg", phase_mask_format = 'grayscale')

F = MonochromaticField(
    wavelength=500 * nm, extent_x=18 * mm, extent_y=18 * mm, Nx=1024, Ny=1024
)

F.add(ApertureFromImage("./grating holo.jpg", image_size=(5 * mm, 5 * mm), simulation = F))
F.add(Lens(f = 20*cm))
#for i in range(1, 160, 1):
F.propagate(20 * cm)
rgb = F.get_colors()
F.plot_colors(rgb, xlim=[-7* mm, 7* mm], ylim=[-7* mm, 7* mm])`)

  const [repoUrl, setRepoUrl] = useState('')

  const handleRunSimulation = () => {
    toast({
      title: "Simulation Started",
      description: "The physics simulation is now running. This may take a few moments.",
    })
    // In a real application, this is where you'd trigger the actual simulation
  }

  const handleSaveToGitHub = () => {
    if (!repoUrl) {
      toast({
        title: "Error",
        description: "Please enter a GitHub repository URL.",
        variant: "destructive",
      })
      return
    }
    toast({
      title: "Saving to GitHub",
      description: `Pushing changes to ${repoUrl}`,
    })
    // In a real application, this is where you'd implement the GitHub integration
  }

  return (
    <Card className="w-full max-w-4xl mx-auto bg-gray-900 text-white">
      <CardHeader>
        <CardTitle className="text-xl flex items-center gap-2">
          <Github className="w-5 h-5" />
          Physics Simulation GitHub Integration
        </CardTitle>
      </CardHeader>
      <CardContent className="space-y-4">
        <div className="space-y-2">
          <Label htmlFor="code-editor">Physics Simulation Code</Label>
          <Textarea
            id="code-editor"
            value={code}
            onChange={(e) => setCode(e.target.value)}
            className="font-mono text-sm h-96 bg-gray-800 border-gray-700"
          />
        </div>
        <div className="flex justify-between items-center">
          <Button onClick={handleRunSimulation} className="flex items-center gap-2">
            <Play className="w-4 h-4" />
            Run Simulation
          </Button>
          <div className="flex items-center gap-2">
            <Input
              placeholder="Enter GitHub repo URL"
              value={repoUrl}
              onChange={(e) => setRepoUrl(e.target.value)}
              className="w-64 bg-gray-800 border-gray-700"
            />
            <Button onClick={handleSaveToGitHub} variant="outline" className="flex items-center gap-2">
              <Save className="w-4 h-4" />
              Save to GitHub
            </Button>
          </div>
        </div>
      </CardContent>
    </Card>
  )
}

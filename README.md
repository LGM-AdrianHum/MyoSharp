MyoSharp
========

C# Wrapper for the Myo Armband

The goal of this project is to allow a high-level object-oriented C# API for devs to easily interact with the Myo.

MyoSharp is compatible with .NET 2.0+

Sample Usage

using MyoSharp.Device;
using MyoSharp.Discovery;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Runtime.InteropServices;
using System.Text;
using System.Threading.Tasks;

namespace MyoSharp
{
    class Program
    {

        static void Main(string[] args)
        {
            var hub = Hub.Create("com.myosharp.myoapp");
            hub.StartListening();

            hub.Paired += hub_Paired;

            Console.ReadLine();
        }

        static void hub_Paired(object sender, MyoEventArgs e)
        {
            e.Myo.PoseChange += Myo_PoseChange;
            e.Myo.Connected += Myo_Connected;
        }

        static void Myo_Connected(object sender, MyoEventArgs e)
        {
            Console.WriteLine("Myo Connected");
        }

        static void Myo_PoseChange(object sender, PoseEventArgs e)
        {
            Console.WriteLine("Pose Detected: " + e.Pose);
        }
    }
}


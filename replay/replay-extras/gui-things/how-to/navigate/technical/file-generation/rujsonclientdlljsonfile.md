---
description: Source code for this function
cover: ../../../../../../../.gitbook/assets/image.avif
coverY: 0
---

# RuJsonClientDLLJSONFile()

{% hint style="info" %}
The function data is kept static to simulate a cheat environment. Normally, this data is remotely fetched and is constantly updated and checked by the program. But to make sure I were not handing out exploit code, I actually wanted to hardcode a bunch of fake and AI generated values based on existing templates for games.\
\
Since REplay was designed to mimick a real world game cheat- the values and offsets were still needed.
{% endhint %}

```cpp

void RunJsonClientFile() {
	// Your JSON data
	const char* jsonData = R"(
     {
  "client_dll": {
    "data": {
      "dwEntityList": {
        "value": 24962720,
        "comment": null
      },
      "dwForceAttack": {
        "value": 23912064,
        "comment": null
      },
      "dwForceAttack2": {
        "value": 23912208,
        "comment": null
      },
      "dwForceBackward": {
        "value": 23912784,
        "comment": null
      },
      "dwForceCrouch": {
        "value": 23913504,
        "comment": null
      },
      "dwForceForward": {
        "value": 23912640,
        "comment": null
      },
      "dwForceJump": {
        "value": 23913360,
        "comment": null
      },
      "dwForceLeft": {
        "value": 23912928,
        "comment": null
      },
      "dwForceRight": {
        "value": 23913072,
        "comment": null
      },
      "dwGameEntitySystem": {
        "value": 26209744,
        "comment": null
      },
      "dwGameEntitySystem_getHighestEntityIndex": {
        "value": 5392,
        "comment": null
      },
      "dwGameRules": {
        "value": 25341336,
        "comment": null
      },
      "dwGlobalVars": {
        "value": 23895208,
        "comment": null
      },
      "dwGlowManager": {
        "value": 25339136,
        "comment": null
      },
      "dwInterfaceLinkList": {
        "value": 26397288,
        "comment": null
      },
      "dwLocalPlayerController": {
        "value": 25287832,
        "comment": null
      },
      "dwLocalPlayerPawn": {
        "value": 23940936,
        "comment": null
      },
      "dwPlantedC4": {
        "value": 25368536,
        "comment": null
      },
      "dwPrediction": {
        "value": 23940624,
        "comment": null
      },
      "dwSensitivity": {
        "value": 25344664,
        "comment": null
      },
      "dwSensitivity_sensitivity": {
        "value": 64,
        "comment": null
      },
      "dwViewAngles": {
        "value": 25759536,
        "comment": null
      },
      "dwViewMatrix": {
        "value": 25349792,
        "comment": null 
      },
      "dwViewRender": {
        "value": 25351912,
        "comment": null
      }
    },
    "comment": "client.dll"
  },
  "engine2_dll": {
    "data": {
      "dwBuildNumber": {
        "value": 5116884,
        "comment": null
      },
      "dwNetworkGameClient": {
        "value": 5114248,
        "comment": null
      },
      "dwNetworkGameClient_getLocalPlayer": {
        "value": 240,
        "comment": null
      },
      "dwNetworkGameClient_maxClients": {
        "value": 592,
        "comment": null
      },
      "dwNetworkGameClient_signOnState": {
        "value": 576,
        "comment": null
      },
      "dwWindowHeight": {
        "value": 5864972,
        "comment": null
      },
      "dwWindowWidth": {
        "value": 5864968,
        "comment": null
      }
    },
    "comment": "engine2.dll"
  },
  "game_info": {
    "data": {
      "buildNumber": {
        "value": 13985,
        "comment": "Game build number"
      }
    },
    "comment": "Some additional information about the game at dump time"
  },
  "inputsystem_dll": {
    "data": {
      "dwInputSystem": {
        "value": 218976,
        "comment": null
      }
    },
    "comment": "inputsystem.dll"
  }
}
    )";

    //system(("echo " + std::string("\"") + currentPath.string() + "\"" + " & pause").c_str());
	std::filesystem::path outputPath = currentPath / "offsets.json";
	std::ofstream outFile(outputPath);
	if (outFile.is_open()) {
		outFile << jsonData << std::endl;
		outFile.close();
       // system("echo 'done' & pause");
	}
	else {
        system("dir");
	}
}
```

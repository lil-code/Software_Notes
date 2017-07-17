# Player controller script

- This script is designed to allow controller functionality on a mobile device
  - "CrossPlatform" == Mobile in this case



File: **playerController.cs**

```CS
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

// THIS PACKAGE IS USED TO ALLOW MOBILE CONTROLLER PREFAB
using UnityStandardAssets.CrossPlatformInput;
// THIS PACKAGE SETS UP THE HEADS UP DISPLAY/ CONTROLLER FOR THE 'GAME'
using UnityEngine.UI;


public class playerController : MonoBehaviour {
  
	private Animation anim;

	private Rigidbody rb;

	// Use this for initialization
	void Start () {
		anim = GetComponent<Animation> ();
		rb = GetComponent<Rigidbody> ();
	}

	// Update is called once per frame
	void Update () {

		float x = CrossPlatformInputManager.GetAxis ("Horizontal");
		float y = CrossPlatformInputManager.GetAxis ("Vertical");

		//transform.position += new Vector3(0,0,y/10);
		//transform.position += new Vector3(x/10,0,0);

		Vector3 movement = new Vector3 (x, 0.0f, y);

		//enter trumps speed here!!!
		rb.velocity = movement * 4f;

		if (x != 0 && y != 0) {
			transform.eulerAngles = new Vector3 (transform.eulerAngles.x, Mathf.Atan2 (x, y) * Mathf.Rad2Deg, transform.eulerAngles.z);
		}

		if (x != 0 || y != 0) {
			anim.Play ("walk");
		} else {
			anim.Play ("idle");
		}
	}
}
```
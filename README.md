C# MONOBEHAVIOUR
// Concept: A game character
represented as data + behavior(a class).
// CODE PROPER
using System;
class character
{
	public string Name;
	public int X,Y;. //position on the map
	public int width, Height; //bounding shape
	public int Health;

	//Constructor: how a character is "born"
	public character(string name, int x, int y, int width, int height, int health)

	{
		Name = name;
		X = x;
		Y = y;
		Width = width;
		Height = height;
		Health = health;
	}
// Behavior: methods define what the character can Do 
     public void MoveTo(int newX, int newY)
	{
		X = newX;
		Y = newY;
		console.WriteLine($"{Name} moved to ({X},{Y})");
	}
	public void TakeDamage(int amount)
	{
		Health -= amount; // Decreased of your health
		Health = Math.Max(Health , 0);
		Console.WriteLine($"{Name} tool {amount} damage.Health:{Health}");
	}
	public void PrintShape()
	{
		//Draw the character as an ASCII rectangle
		for (int row = 0; row < Height' row++)
	}
	Console.WriteLine(new string('#', Width));
}

//Movement for Gridbased character
class Program
{
	static void Main()
	{
		Character hero = new Character("Hero", 0,0, 3, 2, 100);
		hero:PrintShape();
		hero.MoveTo(5 , 3);
		hero.TakeDamage(25);

	}
}
//GRID BASE MOVEMENT 
//GameObject using UnityEngine;
public class GridMovement : MonoBehaviour 
{
	public float tileSize=1.0f; // size of one grid cell
	public float moveSpeed = 10f // how fast we glide between tiles(feel, not logic)
	public Vector3 targetPosition1
	private bool isMoving = false;

	void Start()
	{
		// Snap starting position to the grid so everything lines up
		transform.position = SnapToGrid(transform.position);
		transform.position =targetPosition
	} 
	void update()
	{
		if(!isMoving)'
		{
			HadleInput();
		}
		else
	}
	 //Smoothly guide to the next line
    transform.position=Vector3.MoveTowards(transform.position,targetPosition.moveSpeed * Tile.deltaTime);
     if (Vector 3.Distance(transform.position,targetPosition) <0.001f)
	{
		transform.position = targetPosition;
		isMoving = false;
	}
	
}

  void HadleInput()
{
	 Vector3 direction = Vector3.Zero;

	 if(Input.GetKeyDown(KeyCode.W))direction = Vector3.up;
	 else if(Input.GetKeyDown(KeyCode.S))direction =Vector3.down;
	 else if(Input.GetKeyDown(KeyCode.A))direction =Vector3.left;
	 else if(Input.GetKeyDown(KeyCode.D))direction =Vector3.right;

	 if(direction != Vector3.zero)
    {
		targetPosition =transform.position + direction * tileSize;
		isMoving = true;
	{
		return new Vector3(
			Mathf.Round(pos.x / tileSize) *tileSize,
			Mathf.Round(pos.y / tileSize) *tileSize,
			pos.z
		);
	}
	}
}
//Movement for Freemovement (VECTOR BASED) character
using UnityEngine;
public class FreeMovement: MonoBehaviour
{
	public float moveSpeed 5f;

	void update()
	{
	 // GetAxis give smooth values between -1 and 1
	 float horizontal =Input.GetAxis("Horizontal"); // A/D or LEFT/RIGHT ARROWS
	 float vertical=Input.GetAxis("Vertical"); // W/S or UP/DOWN ARROWS
	 Vector3 direction =new Vector3(horizontal, vertical, Of);
	 // Diagonal movement 
	 if(direction.magnitude > 1f)
	{
		direction.Normalize();
	}
	    transform.position += direction * moveSpeed * Time.deltaTime;
	}
}

//Movement for Physicsbased Character
//GameObject/ rigidbody2D component
using UnityEngine;

[RequireComponent(typeif(rigidbody2D))]
public class PhysicMovement: MonoBehaviour
{
	public float moveForce =10f;
	public float jumpForce = 7f;
	public float maxSpeed = 6f;

	private Rigidbody2D rb;
	private bool isGrounded = false;

	void start()
	{
		rb = GetComponent<Rigidbody2D>();
	}
	void FixedUpdate()
	{
	 //physic change FixedUpdate
	 // frame rate 
	 float horizontal = Input.GetAxis("Horizontal");
	 rb.AddForce(new Vector2(horizontal * moveForce, 0f));
	 // Clam Horizontal
	 if(mathf.abs(rb.velocity.x)> maxSpeed)
	{
		rb.velocity = new Vector2(Mathf.Sign(rb.velocity.x)* maxSpeed, rb.velocity.y);
	}
	}
     void OnCollisionEnter2D(Collision2D collision)
	{
		if (collision.GameObject.CompareTag("Ground"))
		{
		isGrounded = true;
		}
	}
	void OnCollisionExit2D(Collision2D collision)
	{
		if(collision.gameObject.CompareTag("Ground"))
		{
			is Ground = false;
		}
	}
}

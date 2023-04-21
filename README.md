# Lab-8_202001408
The Boa class implementation is housed in a package called Lab08. The corresponding.java code is as follows:

    package Lab08;

    /* represents a Boa Constrictor */
    public class Boa {
	private String name;
	private int length; // the length of the boa, in feet
	private String favoriteFood;

	  public Boa (String name, int length, String favoriteFood) {
		this.name = name;
		this.length = length;
		this.favoriteFood = favoriteFood;
	}
	public boolean isHealthy() {
		/* returns true if this boa constrictor is healthy */
		return this.favoriteFood.equals("granola bars");
	}
	public boolean fitsInCage(int cageLength) {
		/* returns true if the length of this boa constrictor is
	 	  less than the given cage length */
		return this.length < cageLength;
	}
     }
## Creating a JUnit Test Class in Eclipse
JUnit test cases can be added to any.java file by right-clicking the file, selecting new, and then selecting JUnit Test Case. We make the BoaTest.java test case file for the Boa.java file.

The setUp() function is defined after the test case file has been set up.

     package Lab08;
  
      import static org.junit.jupiter.api.Assertions.*;
  
      import org.junit.jupiter.api.AfterAll;
      import org.junit.jupiter.api.AfterEach;
      import org.junit.jupiter.api.BeforeAll;
      import org.junit.jupiter.api.BeforeEach;
      import org.junit.jupiter.api.Test;
  
      class BoaTest {
	      private Boa jen, ken;

	@BeforeEach
	void setUp() throws Exception {
		jen = new Boa("Jennifer", 2, "grapes");
		ken = new Boa("Kenneth", 3, "granola bars");
	}
	@AfterEach
	void tearDown() throws Exception {
	}
	@Test
	final void testIsHealthy() {
		fail("Not yet implemented"); // TODO
	}
	@Test
	final void testFitsInCage() {
		fail("Not yet implemented"); // TODO
	}
    }

>*Note that the methods testIsHealthy() and testFitsInCage() will contain code to test the Boa class methods. These functions along with tearDown() are yet to be implemented.*

## Testing Boa class methods
### *isHealthy() method*
It's crucial to remember that the isHealthy() function has no parameters. As a result, the method can only be called on the Boa objects _"jen" and _"ken" in test situations.
The following are the test cases listed in the testIsHealthy() test function:

    final void testIsHealthy() {
        assertFalse(jen.isHealthy());
        assertTrue(ken.isHealthy());
    }
>The cases are defined so because jen does not have favoriteFood as "granola bar" which is necessary for boa object to be healthy while ken has favoriteFood as "granola bar".

### *FitsInCage() method*
There are numerous test cases that could be possible because the FitsInCage() function accepts an integer parameter as input.
It is preferable to call methods from both instances to guarantee that the function definition is independent of the instance even if jen and ken will both be executing the same function definition for the _FitsInCage(cage_length>) function call.

The test-cases defined can thus go as follows:

    final void testFitsInCage() {
        // invalid length input
       assertFalse(jen.fitsInCage(-1));
       assertFalse(jen.fitsInCage(-3));

    // cage larger than boa
    assertTrue(jen.fitsInCage(10));
    assertTrue(ken.fitsInCage(6));

    // cage smaller than boa
    assertFalse(jen.fitsInCage(0));
    assertFalse(ken.fitsInCage(1));

    // cage length equal to boa
    assertTrue(jen.fitsInCage(2));
    assertTrue(jen.fitsInCage(3));
}
>Here, the test cases will be roughly separated into two partitions, which correspond to the boundary conditions of cage length equal to Boa and lengths less than Boa, more than Boa, and equal to Boa.

>The first two test cases also take into account negative lengths, which are associated with erroneous input for lengths and must always return false.

## Running the Test Cases
To run the test cases, we simply right-click on the file(BoaTest.java here), click on Coverage As, and then 1 JUnit Test.

![image](https://user-images.githubusercontent.com/124348114/233601261-c3aa101d-6530-4923-ad8f-a8dec4777159.png)


>Here, the last two test cases fail indicating an error in the code. The error occurs in the isHealthy() function which is defined as follows:

    public boolean fitsInCage(int cageLength) {
        return this.length < cageLength;
    }
>To correct this error, the actual definition of the function should be like as shown below to account for the fact that the boa can fit in a cage equal to its length (even if not comfortably).

    public boolean fitsInCage(int cageLength) {
        return this.length <= cageLength;
    }
With the modified code, we can see that all the test-case successfully pass now

![image](https://user-images.githubusercontent.com/124348114/233601530-746c5846-0272-40e4-ac87-14edcf33cce5.png)


## Adding new Method
we add a new method lengthInches() to return the length of the Boa in inches.

    public int lengthInches(){
        return this.length * 12;
    }
``
The new test cases defined for the same are as follows:

    final void testLengthInches() {
        assertEquals(jen.lengthInches(), 24);
        assertEquals(ken.lengthInches(), 36);
    }
The test case pass successfully as shown below

![image](https://user-images.githubusercontent.com/124348114/233601694-fa37b113-b1d9-4b74-a203-34b02e9c5411.png)

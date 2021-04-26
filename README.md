# Test Driven Ranges

This exercise extends the [Battery Monitoring] use-case.

The charging current varies during the process of charging.
We need to capture the range of current measurements -
what range of currents are most often encountered while charging.

> **DO NOT** jump into implementation! Read the example and the starting task below.

## Example

### Input

Consider a set of periodic current samples from a charging session to be:
`3, 3, 5, 4, 10, 11, 12`

### Functionality 

The continuous ranges in there are: `3,4,5` and `10,11,12`.

The task is to detect the ranges and
output the number of readings in each range.

In this example,

- the `3-5` range has `4` readings
- the `10-12` range has `3` readings.

### Output

The expected output would be:

```
Range, Readings
3-5, 4
10-12, 3
```

## Tasks

Start test-driven development:

1. Establish quality parameters for your project: What is the maximum complexity you would allow? How much duplication would you consider unacceptable? What is the coverage you'll aim for?
Adapt/adopt/extend the `yml` files from one of your workflow folders.

1. Write the smallest possible failing test.

1. Write the minimum amount of code that'll make it pass.

1. Write the next failing test.

Implement one failing test and at least one passing test:



*******************************************************************************************************



**TEST_CASE_01**("Test the Number of continuous ranges") 
	{

  		float CurrentSamples[]={1,2,3,4,5,6,7};
  		int NumberofReadings=7;
  		int NumberofContRange=0;
  		NumberofContRange=detect_ContRanges_Readings(CurrentSamples,NumberofReadings);
  		REQUIRE(NumberofContRange == 1);
	} 


**Impl_Iteration_01:**

	int detect_ContRanges_Readings(const float* CurrentSamples, int NumberofReadings)
		{

			return 1;
		}



*******************************************************************************************************



**TEST_CASE_02**("Test the Number of continuous ranges > 1") 
	{
	
  		float CurrentSamples[]={1,2,3,4,10,11,12,13};
  		int NumberofReadings=8;
  		int NumberofContRange=0;
		NumberofContRange=detect_ContRanges_Readings(CurrentSamples,NumberofReadings);
  	  	REQUIRE(NumberofContRange == 2);
  
  	}



**Impl_Iteration_02:**

int detect_ContRanges_Readings(const float* CurrentSamples, int NumberofReadings)
{ 
	int NumberofContRange=0;
	int startNum=*CurrentSamples;
	for(int itr=1; itr<NumberofReadings; itr++)
	{
		if((startNum+1)== *(CurrentSamples+itr))
			{
				startNum=*(CurrentSamples+itr);
			}
		else
			{
				NumberofContRange++;
				startNum=*(CurrentSamples+itr);
			}
			
	}
	if(*(CurrentSamples+NumberofReadings-1)-1==*(CurrentSamples+NumberofReadings-2))
		NumberofContRange++;
		
	return NumberofContRange;
}



*******************************************************************************************************



**TEST_CASE_03**("Test the Number of continuous ranges when adjacent values are same") 
{
	
  float CurrentSamples[]={1,3,3,4,10,11,12,13};
  int NumberofReadings=8;
  int NumberofContRange=0;
  
  NumberofContRange=detect_ContRanges_Readings(CurrentSamples,NumberofReadings);
  
  REQUIRE(NumberofContRange == 2);
}



**Impl_Iteration_03:**

int detect_ContRanges_Readings(const float* CurrentSamples, int NumberofReadings)
{ 
	int NumberofContRange=0;
	int startNum=*CurrentSamples;
	for(int itr=1; itr<NumberofReadings; itr++)
	{
		if((startNum+1)== *(CurrentSamples+itr) || (startNum)== *(CurrentSamples+itr))
			{
				startNum=*(CurrentSamples+itr);
			}
		else
			{
				NumberofContRange++;
				startNum=*(CurrentSamples+itr);
			}
			
	}
	if((*(CurrentSamples+NumberofReadings-1)-1==*(CurrentSamples+NumberofReadings-2)) ||\
			(*(CurrentSamples+NumberofReadings-1)==*(CurrentSamples+NumberofReadings-2)))
		NumberofContRange++;
		
	return NumberofContRange;
}



*******************************************************************************************************



**TEST_CASE_04**("Test the Number of continuous ranges when input order is different") 
{
	
  float CurrentSamples[]={1,4,3,5,10,11,12,13};
  int NumberofReadings=8;
  int NumberofContRange=0;
  
  NumberofContRange=detect_ContRanges_Readings(CurrentSamples,NumberofReadings);
  
  REQUIRE(NumberofContRange == 2);
}



**Impl_Iteration_04:**

int detect_ContRanges_Readings(const float* CurrentSamples, int NumberofReadings)
{ 

	1. Short the Input Array in Asscending order
	2. Follow the below impl.

	int NumberofContRange=0;
	int startNum=*CurrentSamples;
	for(int itr=1; itr<NumberofReadings; itr++)
	{
		if((startNum+1)== *(CurrentSamples+itr) || (startNum)== *(CurrentSamples+itr))
			{
				startNum=*(CurrentSamples+itr);
			}
		else
			{
				NumberofContRange++;
				startNum=*(CurrentSamples+itr);
			}
			
	}
	if((*(CurrentSamples+NumberofReadings-1)-1==*(CurrentSamples+NumberofReadings-2)) ||\
			(*(CurrentSamples+NumberofReadings-1)==*(CurrentSamples+NumberofReadings-2)))
		NumberofContRange++;
		
	return NumberofContRange;
}



*******************************************************************************************************



**TEST_CASE_05**("Test the Number of continuous ranges and NumofReadings") 
{
	
  float CurrentSamples[]={1,4,3,5,10,11,12,13};
  int NumberofReadings=8;
  int NumberofContRange=0;
  int ExpNumofReadings[]={4,4};
  
  NumberofContRange=detect_ContRanges_Readings(CurrentSamples,NumberofReadings);
  
  REQUIRE(NumberofContRange == 2);
  
  for(int Itr=0;Itr<NumberofContRange;Itr++),
  {
  REQUIRE(NumberofReadings[Itr] == ExpNumofReadings[Itr]);
  }
}



**Impl_Iteration_05:**

NumberofReadings[10]={4,4,4,4,4,4,4,4,4,4};
int detect_ContRanges_Readings(const float* CurrentSamples, int NumberofReadings)
{ 

	1. Short the Input Array in Asscending order
	2. Follow the below impl.

	int NumberofContRange=0;
	int startNum=*CurrentSamples;
	for(int itr=1; itr<NumberofReadings; itr++)
	{
		if((startNum+1)== *(CurrentSamples+itr) || (startNum)== *(CurrentSamples+itr))
			{
				startNum=*(CurrentSamples+itr);
			}
		else
			{
				NumberofContRange++;
				startNum=*(CurrentSamples+itr);
			}
			
	}
	if((*(CurrentSamples+NumberofReadings-1)-1==*(CurrentSamples+NumberofReadings-2)) ||\
			(*(CurrentSamples+NumberofReadings-1)==*(CurrentSamples+NumberofReadings-2)))
		NumberofContRange++;
		
	return NumberofContRange;
}




*******************************************************************************************************




**TEST_CASE_06**("Test the Number of continuous ranges and NumofReadings") 
{
	
  float CurrentSamples[]={1,4,3,5,10,11,12,13,14};
  int NumberofReadings=8;
  int NumberofContRange=0;
  int ExpNumofReadings[]={4,5};
  
  NumberofContRange=detect_ContRanges_Readings(CurrentSamples,NumberofReadings);
  
  REQUIRE(NumberofContRange == 2);
  
  for(int Itr=0;Itr<NumberofContRange;Itr++),
  {
  REQUIRE(NumberofReadings[Itr] == ExpNumofReadings[Itr]);
  }
}



**Impl_Iteration_06:**
1. Find the number of readings in each range and stroge it in glabal array.



*******************************************************************************************************



**Continue the above process until cover the all Unit TestCases**
.
.
.

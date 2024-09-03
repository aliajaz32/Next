Chapter 8 :

1. Static and Dynamic Rendering.

                Simulating a Slow Data Fetch
2.  In your data.ts file, uncomment the console.log and setTimeout inside fetchRevenue():

3.  in /app/lib/data.ts
   export async function fetchRevenue() {
  try {
    // We artificially delay a response for demo purposes.
    // Don't do this in production :)
    console.log('Fetching revenue data...');
    await new Promise((resolve) => setTimeout(resolve, 3000));
 
    const data = await sql<Revenue>`SELECT * FROM revenue`;
 
    console.log('Data fetch completed after 3 seconds.');
 
    return data.rows;
  } catch (error) {
    console.error('Database Error:', error);
    throw new Error('Failed to fetch revenue data.');
  }
}


3. With dynamic rendering, your application is only as fast as your slowest data fetch.


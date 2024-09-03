Chapter 7

Fetching Data

Fetching data for the dashboard overview page

1. Navigate to /app/dashboard/page.tsx, paste the following code.

import { Card } from '@/app/ui/dashboard/cards';
import RevenueChart from '@/app/ui/dashboard/revenue-chart';
import LatestInvoices from '@/app/ui/dashboard/latest-invoices';
import { lusitana } from '@/app/ui/fonts';
 
export default async function Page() {
  return (
    <main>
      <h1 className={`${lusitana.className} mb-4 text-xl md:text-2xl`}>
        Dashboard
      </h1>
      <div className="grid gap-6 sm:grid-cols-2 lg:grid-cols-4">
        {/* <Card title="Collected" value={totalPaidInvoices} type="collected" /> */}
        {/* <Card title="Pending" value={totalPendingInvoices} type="pending" /> */}
        {/* <Card title="Total Invoices" value={numberOfInvoices} type="invoices" /> */}
        {/* <Card
          title="Total Customers"
          value={numberOfCustomers}
          type="customers"
        /> */}
      </div>
      <div className="mt-6 grid grid-cols-1 gap-6 md:grid-cols-4 lg:grid-cols-8">
        {/* <RevenueChart revenue={revenue}  /> */}
        {/* <LatestInvoices latestInvoices={latestInvoices} /> */}
      </div>
    </main>
  );
}

                        Fetching data for <RevenueChart/>

1. To fetch data for the <RevenueChart/> component, import the fetchRevenue function from data.ts and call it inside your component:

2. Then, uncomment the <RevenueChart/> component, navigate to the component file (/app/ui/dashboard/revenue-chart.tsx) and uncomment the code inside it. Check your localhost, you should be able to see a chart that uses revenue data.

                        Fetching data for <LatestInvoices/>

1. In your page, import the fetchLatestInvoices function:

2. Then, uncomment the <LatestInvoices /> component. You will also need to uncomment the relevant code in the <LatestInvoices /> component itself, located at /app/ui/dashboard/latest-invoices.


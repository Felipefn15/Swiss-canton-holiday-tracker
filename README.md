### [Swiss Canton Holiday Tracker](https://v0-swiss-canton-holiday-tracker.vercel.app/)

## Overview

The Swiss Canton Holiday Tracker is a web application designed to help users in Switzerland optimize their holiday planning based on their unique working schedules and the specific public holiday calendar of their canton.

Switzerland has 26 cantons, each with its own set of public holidays. This application allows users to identify which holidays fall on their working days, helping them plan their time off more effectively.





## 🎯 Purpose

This application empowers users to:

- **Identify Working Day Holidays:** Highlight public holidays that fall on the user's chosen working days, enabling them to understand when they will be off work without needing to take additional leave days.
- **Optimize Leave Planning:** Assist users in planning their vacations or leave by identifying potential long weekends or bridging opportunities. This can help maximize their time off by combining public holidays with their regular days off.


## ✨ Features

### 1. Location, Year, and Work Day Selection

- Choose any of the 26 Swiss cantons
- Select a year (defaults to current year)
- Customize work days (e.g., Monday to Friday but not Wednesday)


### 2. Holiday Visualization

- View all holidays for the selected canton and year
- Highlight holidays that fall on your work days
- See statistics for the whole year and remaining year


### 3. Responsive Design

- Works seamlessly on both mobile and desktop devices
- Remembers your preferences between sessions


### 4. User Experience

- Intuitive interface with clear visual indicators
- Dark/light mode support
- Fast and responsive interactions


## 🛠️ Technical Implementation

### Technologies Used

- **Frontend Framework**: Next.js 14 with App Router
- **Styling**: Tailwind CSS with shadcn/ui components
- **State Management**: React Hooks and Context API
- **Data Persistence**: Local Storage
- **API Integration**: Open Holidays API


### Key Components

- Canton selector with all 26 Swiss cantons
- Year selector with multi-year support
- Customizable work day selector
- Holiday list with visual indicators for work days
- Statistics dashboard showing holiday counts


## 🚀 Getting Started

### Prerequisites

- Node.js 18.x or higher
- npm or yarn


### Installation

1. Clone the repository


```shellscript
git clone https://github.com/Felipefn15/swiss-canton-holiday-tracker.git
cd swiss-canton-holiday-tracker
```

2. Install dependencies


```shellscript
npm install
# or
yarn install
```

3. Run the development server


```shellscript
npm run dev
# or
yarn dev
```

4. Open [http://localhost:3000](http://localhost:3000) in your browser


## 📋 Project Structure

```plaintext
swiss-holiday-tracker/
├── app/                  # Next.js app directory
│   ├── globals.css       # Global styles
│   ├── layout.tsx        # Root layout
│   └── page.tsx          # Home page
├── components/           # React components
│   ├── canton-selector.tsx
│   ├── holiday-list.tsx
│   ├── holiday-stats.tsx
│   ├── holiday-tracker.tsx
│   ├── workday-selector.tsx
│   └── year-selector.tsx
├── hooks/                # Custom React hooks
│   ├── use-holidays.ts   # Holiday data fetching
│   └── use-local-storage.ts # Local storage persistence
└── lib/                  # Utility functions and types
    ├── api.ts            # API integration
    └── types.ts          # TypeScript types
```

## 🔍 Implementation Details

### API Integration

The application uses the Open Holidays API to fetch holiday data for Swiss cantons:

```typescript
// Example API call
const url = `https://openholidaysapi.org/PublicHolidays?countryIsoCode=CH&subdivisionCode=CH-${canton}&validFrom=${startDate}&validTo=${endDate}&languageIsoCode=EN`
```

### State Management

The application uses React's useState and useEffect hooks for local component state, and custom hooks for more complex state management:

```typescript
// Example of the useHolidays hook
export function useHolidays(canton: string, year: number) {
  const [holidays, setHolidays] = useState<Holiday[]>([])
  const [isLoading, setIsLoading] = useState(true)
  const [error, setError] = useState<Error | null>(null)

  useEffect(() => {
    const getHolidays = async () => {
      try {
        setIsLoading(true)
        setError(null)
        const data = await fetchHolidays(canton, year)
        setHolidays(data)
      } catch (err) {
        setError(err instanceof Error ? err : new Error("Failed to fetch holidays"))
      } finally {
        setIsLoading(false)
      }
    }

    getHolidays()
  }, [canton, year])

  return { holidays, isLoading, error }
}
```

## 🔮 Future Enhancements

1. **User Authentication**: Add user authentication to allow users to save their preferences across devices
2. **Multiple Profiles**: Allow users to create multiple profiles for different work schedules
3. **Calendar Export**: Add the ability to export holidays to calendar applications
4. **Notifications**: Add notifications for upcoming holidays
5. **Language Support**: Add support for multiple languages (German, French, Italian, Romansh)


## 📝 Assessment Criteria

This project was developed with the following assessment criteria in mind:

- **Understanding & Implementation of Use Cases**: All user stories implemented with attention to detail
- **Functionality & User Experience**: Intuitive interface with responsive design
- **Code Quality & Problem Solving**: Well-structured code with effective problem-solving approaches
- **Creativity & Design**: Clean, modern design with creative elements enhancing user interaction
- **Documentation**: Comprehensive documentation of code and design decisions
- **Additional Considerations**: Implementation of additional features to enrich the application


## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgements

- [Open Holidays API](https://openholidaysapi.org/) for providing holiday data
- [Next.js](https://nextjs.org/) for the React framework
- [Tailwind CSS](https://tailwindcss.com/) for styling
- [shadcn/ui](https://ui.shadcn.com/) for UI components

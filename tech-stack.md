**Frontend Technology Stack:**
- Framework: Next.js 15 (App Router + Server Components)
- Language: TypeScript 5.6+ (strictly typed)
- Styling: Tailwind CSS 4.0 + CSS Modules
- UI Components: shadcn/ui (primary), Headless UI (fallback), custom (last resort)
- Charts: Recharts (default) → Ch- "Generate a **Recharts** line chart for project progress using **TanStack React Query** + **Zod**, inside a **shadcn Card**, with heights `h-64 sm:h-72 lg:h-80 xl:h-96`, matching monitoring typography."
- "Create a Next.js 15 **GET** route for `/api/projects` with pagination and search; validate with Zod; use Prisma; return `{ success, data, pagination }`."
- "Build a reusable **SummaryCard** (shadcn) matching spacing from `summary-cards.tsx` and responsive font sizes."
- "Add **Google Maps** with markers (@react-google-maps/api), container heights responsive, using `NEXT_PUBLIC_GOOGLE_MAPS_API_KEY`."
- "Wire a **PATCH** `/api/projects/[id]` that validates body with Zod and updates via Prisma; add a `useUpdateProject` mutation with optimistic UI."s 4.4 → D3.js/Observable Plot
- Maps: Google Maps JavaScript API + @react-google-maps/api
- Animations: Framer Motion + Lottie React
- Icons: Lucide React + Heroicons
- PWA: Next-PWA + Workbox

**Backend Technology Stack:**
- Runtime: Node.js 20+ LTS
- Framework: Next.js 15 Route Handlers (REST API)
- Database: PostgreSQL + Prisma ORM
- Authentication: NextAuth.js (JWT + Sessions)
- Authorization: Role-based access control (RBAC)
- Validation: Zod (all inputs/outputs)
- Documentation: OpenAPI 3.1
- Express.js: Only for separate microservices (with Helmet, CORS, Rate Limiting)
# Next.js Modern Web Application

A modern, full-stack web application built with Next.js 15, React 19, and TypeScript, featuring a beautiful UI powered by Tailwind CSS and Radix UI components.

## Features

- ⚡️ Next.js 15 with App Router
- 🎨 Modern UI with Tailwind CSS and Radix UI components
- 📱 Fully responsive design
- 🔒 Built-in contact form with email integration
- 🌙 Dark mode support
- 🔥 TypeScript for type safety
- 📦 Modern development workflow with Bun

## Prerequisites

Before you begin, ensure you have the following installed:
- Node.js 20.x or later
- npm
- Docker (for containerized deployment)

## Getting Started

1. Clone the repository:
```bash
git clone <repository-url>
cd <project-directory>
```

2. Install dependencies:
```bash
npm install
```

3. Set up environment variables:
```bash
cp .env.local.example .env.local
```
Edit `.env.local` and update the following variables:
- Configure your SMTP server details for the contact form
- Add any other required environment variables

4. Start the development server:
```bash
npm run dev
```

The application will be available at `http://localhost:3000`.

## Building for Production

### Local Build

```bash
npm run build
npm start
```

### Docker Build

1. Build the Docker image:
```bash
docker build -t your-app-name .
```

2. Run the container:
```bash
docker run -p 3000:3000 your-app-name
```

## Deployment

### AWS ECS Deployment

1. Push the image to Amazon ECR:
```bash
aws ecr get-login-password --region your-region | docker login --username AWS --password-stdin <your-account-id>.dkr.ecr.us-east-2.amazonaws.com
docker tag thinkbigg-nextjs:latest <your-account-id>.dkr.ecr.us-east-2.amazonaws.com/thinkbigg-nextjs:latest
docker push <your-account-id>.dkr.ecr.us-east-2.amazonaws.com/thinkbigg-nextjs:latest
```

2. Create an ECS task definition and service using the AWS Console or CLI.

## Contact Form Setup

To enable the contact form functionality:

1. Ensure you've copied `.env.local.example` to `.env.local`
2. Update the email configuration in `.env.local` with your email server details
3. If using Gmail, follow the Gmail Setup instructions in the Email Configuration section below
4. The contact form will be automatically enabled once the environment variables are set

## Development Notes

- The application uses Next.js App Router for routing
- Styling is handled through Tailwind CSS with custom configurations
- Components are built using Radix UI primitives for accessibility
- TypeScript is configured for type safety
- ESLint and Prettier are set up for code quality

## Project Structure

```
├── app/                # Next.js app directory
├── components/         # React components
├── hooks/             # Custom React hooks
├── lib/               # Utility functions and configurations
├── public/            # Static assets
├── styles/            # Global styles and Tailwind configurations
└── types/             # TypeScript type definitions
```

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Todo

- Implement blog functionality (currently blocked by redirect issues)
- Add more interactive components
- Enhance testing coverage

## Email Configuration

The application uses Nodemailer for sending emails, with a secure test endpoint for verification.

### Environment Variables

Required variables in `.env.local`

### Gmail Setup
If using Gmail (recommended for development):
1. Enable 2-Step Verification in your Google Account
2. Generate an App Password:
   - Go to Google Account Settings → Security
   - Under "2-Step Verification", click on "App passwords"
   - Select "Mail" and your device
   - Use the generated 16-character password as `EMAIL_PASS`

### Implementation Details

- Email service: `lib/email.ts`
  - Handles SMTP communication via Nodemailer
  - Includes error handling and response formatting
- Test endpoint: `app/api/test-email/route.ts`
  - Verifies email configuration
  - Provides detailed error messages
  - Includes rate limiting

### Security Best Practices

1. Never commit `.env.local` to version control
2. Generate a secure random API key:
   ```bash
   openssl rand -hex 32
   ```
3. Test endpoint automatically disabled in production
4. Use environment-specific email configurations
5. Store sensitive credentials in environment variables only


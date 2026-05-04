# nautilusmain.github.ioimport React, { useMemo, useState } from "react";
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";

function IconBase({ className = "", children, viewBox = "0 0 24 24" }) {
  return (
    <svg
      aria-hidden="true"
      viewBox={viewBox}
      fill="none"
      stroke="currentColor"
      strokeWidth="2"
      strokeLinecap="round"
      strokeLinejoin="round"
      className={className}
    >
      {children}
    </svg>
  );
}

function CheckIcon({ className }) {
  return (
    <IconBase className={className}>
      <path d="M20 6 9 17l-5-5" />
    </IconBase>
  );
}

function ShieldCheckIcon({ className }) {
  return (
    <IconBase className={className}>
      <path d="M12 3l7 3v6c0 5-3.5 8.5-7 9-3.5-.5-7-4-7-9V6l7-3Z" />
      <path d="m9 12 2 2 4-4" />
    </IconBase>
  );
}

function StarIcon({ className }) {
  return (
    <IconBase className={className}>
      <path d="m12 3 2.8 5.7 6.2.9-4.5 4.4 1.1 6.2L12 17.3 6.4 20.2l1.1-6.2L3 9.6l6.2-.9L12 3Z" />
    </IconBase>
  );
}

function CrownIcon({ className }) {
  return (
    <IconBase className={className}>
      <path d="M3 18h18" />
      <path d="m4 18 1.5-9 5 4 3-7 3 7 5-4 1.5 9" />
    </IconBase>
  );
}

function WavesIcon({ className }) {
  return (
    <IconBase className={className}>
      <path d="M2 12c2 0 2-2 4-2s2 2 4 2 2-2 4-2 2 2 4 2 2-2 4-2" />
      <path d="M2 18c2 0 2-2 4-2s2 2 4 2 2-2 4-2 2 2 4 2 2-2 4-2" />
      <path d="M2 6c2 0 2-2 4-2s2 2 4 2 2-2 4-2 2 2 4 2 2-2 4-2" />
    </IconBase>
  );
}

function LockIcon({ className }) {
  return (
    <IconBase className={className}>
      <rect x="4" y="11" width="16" height="10" rx="2" />
      <path d="M8 11V8a4 4 0 1 1 8 0v3" />
    </IconBase>
  );
}

function PhoneIcon({ className }) {
  return (
    <IconBase className={className}>
      <path d="M22 16.9v3a2 2 0 0 1-2.2 2A19.8 19.8 0 0 1 11.2 19a19.3 19.3 0 0 1-6-6A19.8 19.8 0 0 1 2.1 4.2 2 2 0 0 1 4.1 2h3a2 2 0 0 1 2 1.7l.5 3a2 2 0 0 1-.6 1.8l-1.3 1.3a16 16 0 0 0 6.4 6.4l1.3-1.3a2 2 0 0 1 1.8-.6l3 .5a2 2 0 0 1 1.7 2Z" />
    </IconBase>
  );
}

function MailIcon({ className }) {
  return (
    <IconBase className={className}>
      <rect x="3" y="5" width="18" height="14" rx="2" />
      <path d="m3 7 9 6 9-6" />
    </IconBase>
  );
}

function MapPinIcon({ className }) {
  return (
    <IconBase className={className}>
      <path d="M12 21s-6-4.35-6-10a6 6 0 1 1 12 0c0 5.65-6 10-6 10Z" />
      <circle cx="12" cy="11" r="2" />
    </IconBase>
  );
}

const plans = [
  {
    id: "standard",
    name: "Basic Package",
    price: 14,
    icon: ShieldCheckIcon,
    description: "Simple protection for seasonal comfort.",
    features: [
      "1 Heating Tune-Up",
      "1 Cooling Tune-Up",
      "Priority Scheduling",
      "10% OFF Repairs",
    ],
  },
  {
    id: "comfort",
    name: "Standard Comfort Package",
    price: 25,
    icon: ShieldCheckIcon,
    description: "Balanced coverage with added repair value.",
    features: [
      "Everything in Basic Package",
      "1 free minor repair up to $150",
      "15% off repairs",
      "Priority scheduling",
      "Seasonal system performance check",
    ],
  },
  {
    id: "premium",
    name: "Total Comfort Package",
    price: 35,
    icon: StarIcon,
    description: "Better savings and extra coverage.",
    features: [
      "Everything in Standard Comfort Package",
      "2 free minor repairs up to $150 each",
      "15% off repairs",
      "No after-hours diagnostic upcharge",
      "Annual system performance report",
    ],
    popular: true,
  },
  {
    id: "diamond",
    name: "Diamond Comfort Plan",
    price: 55,
    icon: CrownIcon,
    description: "Maximum yearly value and peace of mind.",
    features: [
      "Everything in Total Comfort Package",
      "1 major repair credit up to $500 per year",
      "25% off repairs",
      "1 free capacitor per year",
      "Fastest priority scheduling",
    ],
  },
];

const currency = new Intl.NumberFormat("en-US", {
  style: "currency",
  currency: "USD",
  maximumFractionDigits: 0,
});

function getTodayDateValue() {
  const date = new Date();
  const year = date.getFullYear();
  const month = String(date.getMonth() + 1).padStart(2, "0");
  const day = String(date.getDate()).padStart(2, "0");
  return `${year}-${month}-${day}`;
}

function getPlanById(planId) {
  return plans.find((item) => item.id === planId) ?? plans.find((item) => item.id === "premium") ?? plans[0];
}

function runSelfTests() {
  const todayValue = getTodayDateValue();
  if (!/^\d{4}-\d{2}-\d{2}$/.test(todayValue)) {
    throw new Error("getTodayDateValue must return a YYYY-MM-DD string");
  }

  const fallbackPlan = getPlanById("missing-plan");
  if (!fallbackPlan || fallbackPlan.id !== "premium") {
    throw new Error("getPlanById must fall back to the premium plan when the id is unknown");
  }

  const standardPlan = getPlanById("standard");
  if (!standardPlan || standardPlan.price !== 14) {
    throw new Error("getPlanById must return the matching Basic Package for a known id");
  }

  const comfortPlan = getPlanById("comfort");
  if (!comfortPlan || comfortPlan.price !== 25) {
    throw new Error("getPlanById must return the matching Standard Comfort Package for a known id");
  }

  const premiumPlan = getPlanById("premium");
  if (!premiumPlan || premiumPlan.price !== 35) {
    throw new Error("getPlanById must return the matching Total Comfort Package for a known id");
  }
}

runSelfTests();

export default function NautilusMaintenanceSignup() {
  const [selectedPlan, setSelectedPlan] = useState("premium");
  const [billing, setBilling] = useState("monthly");

  const plan = useMemo(() => getPlanById(selectedPlan), [selectedPlan]);
  const today = useMemo(() => getTodayDateValue(), []);
  const annualPrice = plan.price * 12;
  const dueNow = billing === "monthly" ? plan.price : annualPrice;

  function handleSubmit(event) {
    event.preventDefault();
  }

  return (
    <div className="min-h-screen bg-slate-950 text-white">
      <section className="relative overflow-hidden px-4 py-10 md:px-8 lg:px-12">
        <div className="absolute inset-0 opacity-20 bg-[radial-gradient(circle_at_top_left,_#86efac,_transparent_35%),radial-gradient(circle_at_bottom_right,_#1d4ed8,_transparent_35%)]" />
        <div className="relative mx-auto max-w-6xl">
          <div className="mb-8 flex flex-col gap-4 md:flex-row md:items-center md:justify-between">
            <div className="flex items-center gap-4">
              <img src="/mnt/data/Main Logo Version 1.png" alt="Nautilus HVAC & Consulting logo" className="h-16 w-16 rounded-2xl object-contain bg-white/10 p-1 ring-1 ring-emerald-300/30" />
              <div>
                <p className="text-sm uppercase tracking-[0.25em] text-emerald-200">Nautilus HVAC</p>
                <h1 className="text-2xl font-bold">Maintenance Plan Signup</h1>
                <p className="mt-1 text-sm text-slate-300">Call or text 770-560-0250</p>
              </div>
            </div>
            <div className="rounded-full border border-white/15 bg-white/10 px-4 py-2 text-sm text-slate-200 backdrop-blur">
              Moving forward together
            </div>
          </div>

          <div className="mb-6 rounded-3xl border border-emerald-300/20 bg-white/5 p-4 text-sm text-slate-200 shadow-xl shadow-emerald-950/20">
            <div className="flex flex-col gap-2 md:flex-row md:items-center md:justify-between">
              <div>
                <p className="font-semibold text-white">Nautilus HVAC & Consulting</p>
                <p>Professional maintenance memberships with priority scheduling and secure recurring billing.</p>
              </div>
              <div className="text-sm md:text-right">
                <p><a href="tel:7705600250" className="font-semibold text-emerald-300 hover:text-emerald-200">770-560-0250</a></p>
                <p><a href="https://nautilushvac.com" target="_blank" rel="noreferrer" className="font-semibold text-emerald-300 hover:text-emerald-200">nautilushvac.com</a></p>
              </div>
            </div>
          </div>

          <div className="grid gap-8 lg:grid-cols-[1.05fr_0.95fr]">
            <div>
              <div className="mb-6 max-w-2xl">
                <h2 className="text-4xl font-black tracking-tight md:text-5xl">
                  Protect your comfort with automatic monthly maintenance coverage.
                </h2>
                <p className="mt-4 text-lg text-slate-300">
                  Choose your plan, enter your service details, and set up secure recurring payments for your home comfort protection.
                </p>
              </div>

              <div className="grid gap-4 md:grid-cols-2 xl:grid-cols-4">
                {plans.map((item) => {
                  const Icon = item.icon;
                  const active = selectedPlan === item.id;

                  return (
                    <button
                      type="button"
                      key={item.id}
                      onClick={() => setSelectedPlan(item.id)}
                      aria-pressed={active}
                      className={`relative rounded-3xl border p-5 text-left transition hover:-translate-y-1 hover:bg-white/10 ${
                        active ? "border-emerald-300 bg-emerald-300/10 shadow-2xl shadow-emerald-950" : "border-white/15 bg-white/5"
                      }`}
                    >
                      {item.popular ? (
                        <span className="absolute right-4 top-4 rounded-full bg-emerald-300 px-3 py-1 text-xs font-bold text-slate-950">
                          Popular
                        </span>
                      ) : null}
                      <Icon className="mb-4 h-7 w-7 text-emerald-300" />
                      <h3 className="text-lg font-bold">{item.name}</h3>
                      <p className="mt-2 text-sm text-slate-300">{item.description}</p>
                      <div className="mt-4 flex items-end gap-1">
                        <span className="text-3xl font-black">{currency.format(item.price)}</span>
                        <span className="mb-1 text-sm text-slate-400">/mo</span>
                      </div>
                    </button>
                  );
                })}
              </div>

              <Card className="mt-6 rounded-3xl border-white/10 bg-white/5 text-white shadow-2xl">
                <CardContent className="p-6">
                  <div className="mb-4 flex items-center justify-between gap-4">
                    <div>
                      <h3 className="text-xl font-bold">{plan.name}</h3>
                      <p className="text-sm text-slate-300">Included with this plan:</p>
                    </div>
                    <div className="rounded-2xl bg-white/10 px-4 py-3 text-right">
                      <p className="text-2xl font-black">{currency.format(plan.price)}</p>
                      <p className="text-xs text-slate-400">monthly</p>
                    </div>
                  </div>
                  <div className="grid gap-3 sm:grid-cols-2">
                    {plan.features.map((feature) => (
                      <div key={feature} className="flex gap-2 text-sm text-slate-200">
                        <CheckIcon className="mt-0.5 h-4 w-4 shrink-0 text-emerald-300" />
                        <span>{feature}</span>
                      </div>
                    ))}
                  </div>
                </CardContent>
              </Card>
            </div>

            <Card className="rounded-3xl border-white/10 bg-white text-slate-950 shadow-2xl">
              <CardContent className="p-6 md:p-8">
                <div className="mb-6">
                  <h2 className="text-2xl font-black">Start Your Plan</h2>
                  <p className="mt-2 text-sm text-slate-600">
                    This form is designed to connect to Stripe, Square, or another payment processor for secure recurring payments.
                  </p>
                </div>

                <form className="space-y-5" onSubmit={handleSubmit}>
                  <div className="grid gap-4 sm:grid-cols-2">
                    <label className="space-y-2">
                      <span className="text-sm font-semibold">First Name</span>
                      <input
                        name="firstName"
                        autoComplete="given-name"
                        className="w-full rounded-2xl border border-slate-200 px-4 py-3 outline-none focus:border-emerald-500"
                        placeholder="Jonathan"
                      />
                    </label>
                    <label className="space-y-2">
                      <span className="text-sm font-semibold">Last Name</span>
                      <input
                        name="lastName"
                        autoComplete="family-name"
                        className="w-full rounded-2xl border border-slate-200 px-4 py-3 outline-none focus:border-emerald-500"
                        placeholder="Jackson"
                      />
                    </label>
                  </div>

                  <div className="grid gap-4 sm:grid-cols-2">
                    <label className="space-y-2">
                      <span className="text-sm font-semibold">Phone</span>
                      <div className="relative">
                        <PhoneIcon className="absolute left-3 top-3.5 h-5 w-5 text-slate-400" />
                        <input
                          name="phone"
                          type="tel"
                          autoComplete="tel"
                          className="w-full rounded-2xl border border-slate-200 py-3 pl-11 pr-4 outline-none focus:border-emerald-500"
                          placeholder="(770) 560-0250"
                        />
                      </div>
                    </label>
                    <label className="space-y-2">
                      <span className="text-sm font-semibold">Email</span>
                      <div className="relative">
                        <MailIcon className="absolute left-3 top-3.5 h-5 w-5 text-slate-400" />
                        <input
                          name="email"
                          type="email"
                          autoComplete="email"
                          className="w-full rounded-2xl border border-slate-200 py-3 pl-11 pr-4 outline-none focus:border-emerald-500"
                          placeholder="customer@email.com"
                        />
                      </div>
                    </label>
                  </div>

                  <label className="block space-y-2">
                    <span className="text-sm font-semibold">Service Address</span>
                    <div className="relative">
                      <MapPinIcon className="absolute left-3 top-3.5 h-5 w-5 text-slate-400" />
                      <input
                        name="serviceAddress"
                        autoComplete="street-address"
                        className="w-full rounded-2xl border border-slate-200 py-3 pl-11 pr-4 outline-none focus:border-emerald-500"
                        placeholder="Street, city, state, ZIP"
                      />
                    </div>
                  </label>

                  <div className="grid gap-4 sm:grid-cols-2">
                    <label className="space-y-2">
                      <span className="text-sm font-semibold">Preferred Start Date</span>
                      <input
                        name="startDate"
                        type="date"
                        defaultValue={today}
                        className="w-full rounded-2xl border border-slate-200 px-4 py-3 outline-none focus:border-emerald-500"
                      />
                    </label>
                    <label className="space-y-2">
                      <span className="text-sm font-semibold">Number of Systems</span>
                      <select
                        name="systems"
                        defaultValue="1"
                        className="w-full rounded-2xl border border-slate-200 px-4 py-3 outline-none focus:border-emerald-500"
                      >
                        <option value="1">1 System</option>
                        <option value="2">2 Systems</option>
                        <option value="3">3 Systems</option>
                        <option value="4+">4+ Systems</option>
                      </select>
                    </label>
                  </div>

                  <div className="rounded-3xl bg-slate-100 p-4">
                    <p className="mb-3 text-sm font-bold">Billing Option</p>
                    <div className="grid gap-3 sm:grid-cols-2">
                      <button
                        type="button"
                        onClick={() => setBilling("monthly")}
                        aria-pressed={billing === "monthly"}
                        className={`rounded-2xl border px-4 py-3 text-left ${
                          billing === "monthly" ? "border-emerald-500 bg-white" : "border-transparent bg-slate-200"
                        }`}
                      >
                        <p className="font-bold">Monthly</p>
                        <p className="text-sm text-slate-600">{currency.format(plan.price)}/month</p>
                      </button>
                      <button
                        type="button"
                        onClick={() => setBilling("annual")}
                        aria-pressed={billing === "annual"}
                        className={`rounded-2xl border px-4 py-3 text-left ${
                          billing === "annual" ? "border-emerald-500 bg-white" : "border-transparent bg-slate-200"
                        }`}
                      >
                        <p className="font-bold">Annual</p>
                        <p className="text-sm text-slate-600">{currency.format(annualPrice)}/year</p>
                      </button>
                    </div>
                  </div>

                  <div className="rounded-3xl border border-slate-200 p-4">
                    <div className="mb-4 flex items-center gap-2">
                      <LockIcon className="h-5 w-5 text-emerald-600" />
                      <p className="font-bold">Secure Payment Setup</p>
                    </div>
                    <div className="space-y-3">
                      <input
                        name="cardNumber"
                        inputMode="numeric"
                        autoComplete="cc-number"
                        className="w-full rounded-2xl border border-slate-200 px-4 py-3 outline-none focus:border-emerald-500"
                        placeholder="Card number"
                      />
                      <div className="grid grid-cols-2 gap-3">
                        <input
                          name="cardExpiration"
                          inputMode="numeric"
                          autoComplete="cc-exp"
                          className="w-full rounded-2xl border border-slate-200 px-4 py-3 outline-none focus:border-emerald-500"
                          placeholder="MM / YY"
                        />
                        <input
                          name="cardSecurityCode"
                          inputMode="numeric"
                          autoComplete="cc-csc"
                          className="w-full rounded-2xl border border-slate-200 px-4 py-3 outline-none focus:border-emerald-500"
                          placeholder="CVC"
                        />
                      </div>
                    </div>
                    <p className="mt-3 text-xs text-slate-500">
                      On a live website, card fields should be replaced with Stripe Elements or Square Web Payments SDK. Do not store card numbers directly.
                    </p>
                  </div>

                  <div className="rounded-3xl bg-slate-950 p-5 text-white">
                    <div className="flex items-center justify-between gap-4">
                      <span className="text-slate-300">Selected Plan</span>
                      <span className="text-right font-bold">{plan.name}</span>
                    </div>
                    <div className="mt-2 flex items-center justify-between gap-4">
                      <span className="text-slate-300">Due Today</span>
                      <span className="text-3xl font-black">{currency.format(dueNow)}</span>
                    </div>
                    <div className="mt-2 space-y-1 text-xs text-slate-400">
                      <p>Recurring payments continue until canceled according to the maintenance agreement terms.</p>
                      <p>Free repairs are available only after 3 full months of active enrollment.</p>
                      <p>Major repair coverage is limited to 1 major repair per year.</p>
                    </div>
                  </div>

                  <div className="rounded-2xl border border-amber-200 bg-amber-50 p-4 text-sm text-amber-900">
                    <p className="font-bold">Plan Disclaimers</p>
                    <ul className="mt-2 list-disc space-y-1 pl-5">
                      <li>Customer must be enrolled for 3 months before claiming any free repairs.</li>
                      <li>Major repair coverage is limited to 1 major repair per year.</li>
                    </ul>
                  </div>

                  <label className="flex gap-3 text-sm text-slate-600">
                    <input name="terms" type="checkbox" className="mt-1" />
                    <span>
                      I agree to the Nautilus HVAC maintenance plan terms, recurring payment authorization, and repair coverage limits.
                    </span>
                  </label>

                  <Button type="submit" className="w-full rounded-2xl bg-emerald-600 py-6 text-base font-bold hover:bg-emerald-700">
                    Start My Maintenance Plan
                  </Button>
                </form>
              </CardContent>
            </Card>
          </div>
        </div>
      </section>
    </div>
  );
}

#!/usr/bin/env ruby
require 'rubygems'
require 'polyglot'
require 'treetop'
require 'colored'

Treetop.load "simple"

parser = SimpleParser.new
exprs = {
  "" => false,
  "value" => true,
  "(((value)))" => true,
  "value*value" => true,
  "value * value" => true,
  "(value * value)" => true,
  "value * value*value" => true,
  "value * value*value*value * value*value" => true,
  "value / value" => true,
  "(value / value)" => true,
  "value/value" => true,
  "value / value / value" => false,
  "value/value/ value" => false,
  "value/value * value" => false,
  "(value/value) * value" => true,
  "(value/value/value) * value" => false,
  "value/(value * value)" => true,
  "value + value" => true,
  "1" => true,
  "12" => true,
  "012" => false,
  "12." => false,
  ".456" => true,
  "0.456" => true,
  "12.5" => true,
  "12.5 * 852 * value" => true,
  "12.5 / 852 * value" => false,
  "self.a" => true,
  "self.ab" => true,
  "self.abc" => true,
  "self.temperature" => true,
  "self._temperature" => false,
  "self.temperature_" => false,
  "self.grains_count" => true,
  "self:temperature" => false,
  "self::temperature" => true,
  "value * self.temperature" => true,
  "value * self.temperature / 1000" => false,
  "value / self.temperature * 1000" => false,
  "value / (self.temperature * 1000)" => true,
  "value / self.temperature / 1000" => false,
  "value / self::net_mass / 1000" => false,
  "(value + self::net_mass) / 1000 + 852" => false,
  "(value + self::net_mass) / 1000 + (852)" => false,
  "((value + self::net_mass) / 1000) + 852" => true,
  "(0.0001 * (value + self::net_mass) * 2) + 852" => true,
  "(0.0001 * (value + self::net_mass) * 2) + 852" => true,
  "(((value * self.thousand_grains_mass) / 1000) * cultivation.net_surface_area) / self::net_mass" => true,
}

for expr, success in exprs
  print ((success ? expr.yellow : expr.magenta) + ":").ljust(exprs.keys.map(&:size).max + 11)
  result = parser.parse(expr)
  message = result.inspect.gsub(/^/, '  ')
  if !result.nil? == success
    puts "[" + " OK ".green + "]"
    # puts message.green unless result.nil?
  else
    puts "[" + "FAIL".red + "]"
    # puts message.red
  end
end
